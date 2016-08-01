---
title: Handling Audio in iOS
date: 2016-06-03 21:01:38
tags:
---
## Leveraging AVFoundation Audio APIs
Its not a rare occurrence when you will have to deal with Audio data in your iOS apps. Lets take a look at how we can use the AVFoundation framework to play, restart, stop, pause audio file in our iOS apps. We will even have a look at how we can manipulate with the audio timings, ie go back/front to a specific time and play the audio from there.

<!-- more -->

## Follow step by step, one at a time
* Drag and drop 4 buttons on the storyboard scene from the object library and style and position the segment control the way you want, the 4 buttons are start, restart, play(pause), stop. Also drag and drop a slider onto the screen. The first button is use to load the music and start playing it. Its used for nothing else. The other 3 buttons will be the most used ones. The restart button will take the music to start and play it from first, the play(pause) is a single toggle button that is use for playing and pausing, the stop button will take the music to start and stop playing it.
* Now lets add the outlet and the actions, add an outlet for the play(pause) button because we will be changing the button title as we play and pause the music file. Add 3 actions for the restart, stop and the start button. Add an outlet and an action(changeAudioTime) for the slider.
* Get the path of the music file by using the following code.
```swift
let path = NSBundle.mainBundle().pathForResource("musicname", ofType: "mp3")
```
* Once you have the path of the resource create an instance of NSURL from the path
```swift
let audioUrl = NSURL(fileURLWithPath: path)
```
* Next we need to import the AVFoundation framework in the view controller file, this allows us to use the speakers on the iphone to play the music file that we have. There are 2 steps to be done here 1st is to place the code `import AVFoundation` in top of view controller file and the other step is to click on the project settings in the file explorer, the go to build phases, and make sure you are selected on target, the click the + button in link binary with libraries, type AVFoundation in the dialog and click add.
* Next step is to create a audio player and give it the contents of the music file that we have with us.
* To start playing the music we can call the play method on the audio player, to pause playing the music we can call the stop method on the audio player, to change the timings of the music we can use the currentTime property of the audio player.
* In the code below we start playing the music once the view is loaded into the memory, we can't present the alert controller here because it can be presented only when the view controller hierarchy is set up, that is why we present the alert controller in the viewDidAppear method which is called after the view hierarchy is setup, ie after the views appear on the screen.
* Always remember that you must stop playing the audio before manipulating with the currentTime of the audio player.

```swift
import UIKit
import AVFoundation

class ViewController: UIViewController {

    @IBOutlet weak var pauseOrPlayButton: UIButton!
    
    @IBOutlet weak var audioTimer: UISlider!
    
    let audioPlayer: AVAudioPlayer? = {
        if let audioPath = NSBundle.mainBundle().pathForResource("audio", ofType: "wav") {
            let audioUrl = NSURL(fileURLWithPath: audioPath)
            
            do {
                let player = try AVAudioPlayer(contentsOfURL: audioUrl)
                return player
            } catch let error as NSError {
                print(error.localizedDescription)
                return nil
            }

        } else {
            print("Music file not found.")
            return nil

        }
    }()
    
    override func preferredStatusBarStyle() -> UIStatusBarStyle {
        return .LightContent
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        //Set a custom image for the slider circle for both the states
        audioTimer.setThumbImage(UIImage(named: "slider-thumbnail"), forState: .Normal)
        audioTimer.setThumbImage(UIImage(named: "slider-thumbnail"), forState: .Highlighted)
        
        
        if let player = audioPlayer {
            player.play()
            //duration property is of type NSTimeInterval aka Double, therefore convert it to float
            audioTimer.maximumValue = Float(player.duration)
        }
        
        //Every 0.1 seconds iOS will call the updateAudioTimer method to keep the slider in sync
        NSTimer.scheduledTimerWithTimeInterval(0.1, target: self, selector: #selector(ViewController.updateAudioTimer), userInfo: nil, repeats: true)
    }
    
    override func viewDidAppear(animated: Bool) {
        super.viewDidAppear(animated)
        
        if audioPlayer == nil {
            let alert = UIAlertController(title: "Opps", message: "Audio Error", preferredStyle: .Alert)
            alert.addAction(UIAlertAction(title: "Ok", style: .Default, handler: nil))
            presentViewController(alert, animated: true, completion: nil)
        }
    }

    @IBAction func restartAudio(sender: AnyObject) {
        if let player = audioPlayer {
            player.stop()
            player.currentTime = 0
            player.play()
        }
    }
    
    @IBAction func pauseOrPlayAudio(sender: AnyObject) {
        if let player = audioPlayer {
            if player.playing {
                //User pressed the pause button
                player.stop()
                pauseOrPlayButton.setTitle("Play", forState: .Normal)
            } else {
                player.play()
                pauseOrPlayButton.setTitle("Pause", forState: .Normal)
            }
        }
    }

    @IBAction func stopAudio(sender: AnyObject) {
        if let player = audioPlayer {
            player.stop()
            player.currentTime = 0
            pauseOrPlayButton.setTitle("Play", forState: .Normal)
        }
    }

    @IBAction func changeAudioTime(sender: AnyObject) {
        if let player = audioPlayer {
            player.stop()
            player.currentTime = NSTimeInterval(audioTimer.value)
            //player.prepareToPlay()
            player.play()
        }
    }
    
    func updateAudioTimer() {
        if let player = audioPlayer {
            //currentTime property is of type NSTimeInterval aka Double, therefore convert it to float
            audioTimer.value = Float(player.currentTime)
        }
    }
}
```
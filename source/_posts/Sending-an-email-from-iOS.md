---
title: Sending an email from iOS
date: 2016-08-02 00:19:30
tags:
---
## It's all about delegation
A simple task of sending an email is also achieved in iOS through the delegation pattern. The basic concept is that we create an email view controller where the user can type the email details and set its delegate to which it will respond back with the results once the user has finished.

<!-- more -->
## Procedure Breakdown
* 1st step would be to design the mail form on the storyboard scene and add the subject,body fields as outlets and connect the send mail button as an a action
* Now we need to import the `MessageUI` framework to send a mail from the view controller, the MessageUI framework en composes all the email related classes and protocols
* Also make the view controller to conform to the `MFMailComposeViewControllerDelegate`, what we are actually doing is we will be presenting a view controller that will be responsible for sending the email and that controller will respond back to its delegate with information such as mail was sent successfully, mail was canceled, error in sending email etc, so we are essentially conforming to the delegate protocol as we want our view controller to be the delegate of that mail controller which we present eventually
* Now the next step would be to create the mail view controller will the subject, recipients, body
* Next we set the delegate of this newly created mail controller to be the view controller itself
* Now we present the mail controller on the screen
* Now we add the delegate methods to which the mail controller will respond back with information

```swift
import Foundation
import UIKit
import MessageUI
 
class ViewController: UIViewController {
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    
    @IBAction func sendEmailButtonTapped(sender: AnyObject) {
        let mailComposeViewController = configuredMailComposeViewController()
        if MFMailComposeViewController.canSendMail() {
            self.presentViewController(mailComposeViewController, animated: true, completion: nil)
        } else {
            self.showSendMailErrorAlert()
        }
    }
    
    func configuredMailComposeViewController() -> MFMailComposeViewController {
        let mailComposeViewController = MFMailComposeViewController()

        // Extremely important to set the --mailComposeDelegate-- property, NOT the --delegate-- property
        mailComposeViewController.mailComposeDelegate = self 
        
        mailComposeViewController.setToRecipients(["someone@somewhere.com"])
        mailComposeViewController.setSubject("Sending you an in-app e-mail...")
        mailComposeViewController.setMessageBody("Sending e-mail in-app is not so bad!", isHTML: false)
        
        return mailComposeViewController
    }
    
    func showSendMailErrorAlert() {
        let sendMailErrorAlert = UIAlertView(title: "Could Not Send Email", message: "Your device could not send e-mail.  Please check e-mail configuration and try again.", delegate: self, cancelButtonTitle: "OK")
        sendMailErrorAlert.show()
    }
}

//Conform to the MFMailComposeViewControllerDelegate protocol
extension ViewController: MFMailComposeViewControllerDelegate {
	func mailComposeController(controller: MFMailComposeViewController!, didFinishWithResult result: MFMailComposeResult, error: NSError!) {
    	switch (result) {
	        
	        case MFMailComposeResultSent:
	            print("The email message was queued in the user’s outbox. It is ready to send the next time the user connects to email.")
	        
	        case MFMailComposeResultSaved:
	            print("The email message was saved in the user’s Drafts folder.")
	        
	        case MFMailComposeResultCancelled:
	            print("The user canceled the operation. No email message was queued.")
	        
	        case MFMailComposeResultFailed:
	            print("The email message was not saved or queued, possibly due to an error.")
	        
	        default:
	            print("An error occurred when trying to compose this email")
	    }
        controller.dismissViewControllerAnimated(true, completion: nil)
    }
}
```
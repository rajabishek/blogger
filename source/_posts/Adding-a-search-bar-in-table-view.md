---
title: Adding a search bar in table view
date: 2016-08-04 16:54:43
tags:
---

## Filtering & Searching information
If you have a large dataset to present, scrolling through a large list becomes slow and frustrating. In that case, it’s essential that we allow users to search for specific items. UISearchController which seamlessly integrates with UITableView allows for quick, responsive filtering of information and solves the very same problem.

<!-- more -->

* Create a UISearchController instance as an instance of the view controller, give the searchResultsController while creating as nil meaning we would like to use the same table for search results also
* Set the searchResultsUpdater property of search controller as self(view controller), meaning view controller would be responsible for updating the search results for the search controller. View controller has to conform to UISearchResultsUpdating protocol.
* Set the dimsBackgroundDuringPresentation property on search controller to false, usually the search controller will dim the background while showing the search results, but since we are using the same table view to show the results we would not want this behavior.
* On the view controller set the definesPresentationContext property to true, it means that the search bar must be hidden when navigating away from the view controller even though it is currently active.
* Set the scope button titles for the search bar
* Set the delegate of the search bar to the view controller. View controller has to conform to UISearchBarDelegate protocol.
* Add the search bar as the header of the table view
* updateSearchResultsForSearchController method is called every time a user changes the contents if the search bar text. It is method of the UISearchResultsUpdating protocol, it is the only compulsory method of the protocol.
* selectedScopeButtonIndexDidChange method is called every time a different scope button is pressed. This method is from the UISearchBarDelegate protocol, however it is not a compulsory method.
```swift
import UIKit

class DevicesTableViewController: UITableViewController {
    
    let devices = [Device(name: "Iphone 5c", type: "Mobile"), Device(name: "Oneplus x", type: "Mobile"), Device(name: "Macbook Pro", type: "Laptop"), Device(name: "Apple Watch", type: "Watch"), Device(name: "Moto 360", type: "Watch"), Device(name: "Samsung Galaxy", type: "Mobile"), Device(name: "Dell Vostro", type: "Laptop"), Device(name: "Dell Inspiron", type: "Laptop")]
    
    var filteredDevices = [Device]()
    
    let searchController = UISearchController(searchResultsController: nil)
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        searchController.searchResultsUpdater = self
        searchController.dimsBackgroundDuringPresentation = false
        definesPresentationContext = true
        searchController.searchBar.scopeButtonTitles = ["All", "Mobile", "Laptop", "Watch"]
        searchController.searchBar.delegate = self
        tableView.tableHeaderView = searchController.searchBar
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }

    // MARK: - Table view data source
    override func numberOfSectionsInTableView(tableView: UITableView) -> Int {
        return 1
    }

    override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        if searchController.active {
            return filteredDevices.count
        }
        return devices.count
    }

    override func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCellWithIdentifier("Cell", forIndexPath: indexPath)

        // Configure the cell...
        let device = searchController.active ? filteredDevices[indexPath.row] : devices[indexPath.row]
        cell.textLabel?.text = device.name
        cell.detailTextLabel?.text = device.type

        return cell
    }
}

extension DevicesTableViewController: UISearchResultsUpdating, UISearchBarDelegate {
    
    func filterContentForSearchText(searchText: String, scope: String = "All") {
        
        if searchText == "" {
            filteredDevices = devices.filter { device in
                return (scope == "All") || (device.type == scope)
            }
        } else {
            filteredDevices = devices.filter { device in
                let categoryMatch = (scope == "All") || (device.type == scope)
                return categoryMatch && device.name.lowercaseString.containsString(searchController.searchBar.text!.lowercaseString)
            }
        }
        
        tableView.reloadData()
    }
    
    func updateSearchResultsForSearchController(searchController: UISearchController) {
        let searchBar = searchController.searchBar
        let scope = searchBar.scopeButtonTitles![searchBar.selectedScopeButtonIndex]
        filterContentForSearchText(searchController.searchBar.text!, scope: scope)
    }
    
    func searchBar(searchBar: UISearchBar, selectedScopeButtonIndexDidChange selectedScope: Int) {
        let searchBar = searchController.searchBar
        let scope = searchBar.scopeButtonTitles![searchBar.selectedScopeButtonIndex]
        filterContentForSearchText(searchController.searchBar.text!, scope: scope)
    }
}
```
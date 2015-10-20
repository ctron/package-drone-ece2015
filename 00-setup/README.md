## Setup

 * Download and install Package Drone
 * Startup and connect to <http://localhost:8080> or wherever you installed it
 
### Creating a user

 * Log in using the admin token
 * Create a user
   * Assign the `MANAGER` and `ADMIN` role
   * Set a password
   
### Setup mail service

 * Click on "Tasks" icon in the header
 * Enter mail server information
 * Click "Update"
 
## Simple manual example

A first example showing the basics.

### Creating a channel

 * Click on "Create Channel" in the channel view
 * Enter the name "osgi1"
 * Click "Create"

### Upload files 

 * Switch to the channel
 * Drop files from `data/00`
 
### Adding functionality

 * Add "Hasher" aspect
 * Add "OSGi" aspect

### Make a P2 repository

 * Add "P2 metadata generator"
 * Add "P2 repository aspect"
 * Check repository

### Adding OSGi R5/OBR support

 * Add "OSGi R5 repository" aspect
 
### Create a virtual feature and category

 * Use "Add artifact" to create a new generated feature
 * Use "Add artifact" to create a new generated category

No matter where the meta data comes from, it is always processed the same way.
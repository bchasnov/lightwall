# Web Interface for the LightWall
There are three modes to run through the Web Interface

1. Student/teacher access for uploading images and code
2. Admin access to manage everything
3. Interactive page for the actual display (should this be in faceserver or web?)

## 1. Student/teacher access
### Basic Requirements
* Google authetication
* Upload >5 headshot photos 
* Live code to draw on canvas
* Save code

### Stretch goal
* Crop group photos
 * Photos are required to only have one face. People may only have group photos of themselves
* Facebook upload photo
* Experiment with face recognition webcam photo
 * HARD because requires remote access to local faceserver machine

## 2. Admin access
### Basic Requirements
* View all student/teacher photos and code
* Manage MongoDB database (Compass)

## 3. Interactive page
## Description
The interactive page is run at the control panel for the lighting display. It can only be viewed in the local network.

## Requirements
Two pages
* Innactive (webcam face tracking output)
* Active (face detected and linked with user)

### Stretch goal
* Detect new user and sends new user email
 * Requires web scraping of student images and emails

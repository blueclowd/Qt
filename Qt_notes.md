# Qt notes

##### {project name}.pro
 - Set the path of libraries in .pro by **INCLUDEPATH** and **LIBS**, it can be manually appened or by Qt creator plugin: right click the project name and select "Add Library...".
 
##### qml.qrc
  - The paths of resourses such as images are described in *qml.qrc*.
  - If having an image folder named "images", using the **source: "images/xxx.png"** in *.qml* to refer to the images under the folder.
  
#####  MouseArea
  - **anchors.fill = XXX** is mandatory.
  
##### Signals & slots
  - Slots receive the event fired by signals.
  - All the classes which inherit class *QObject* can define signals and slots
  - Signals and slots are independent, i.e., they don't see each other.
  - Flows: 
    + The signal is emitted.
    + All slots connected to the emitted signal are executed one after another.
    + Once all the slots are finished, continue the subsequent works after the the place where emitted the signal.
  
##### QImage & QPixmap
- Use *QImage* when image processing is necessary. Use *QPixmap* for display.
- Use *QQuickImageProvider* to display the image in *.qml* to take the advantage of independent threads.

> Should you have any questions about this content, please email me via: lhungting@gmail.com









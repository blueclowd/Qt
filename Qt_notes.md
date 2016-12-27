# Qt notes
> Should you have any questions about this content, please email me via: lhungting@gmail.com

##### {project name}.pro
 - Set the path of libraries in .pro by **INCLUDEPATH** and **LIBS**, it can be manually appened or by Qt creator plugin: right click the project name and select "Add Library...".
 - Add ```QT += widgets serialport``` if you want to use **QtSerialPort** library.
 - Exmaple .pro including pylon5 and OpenCV on MacOS
 
##### qml.qrc
  - The paths of resourses such as images are described in *qml.qrc*.
  - If having an image folder named "images", using the ```source: "images/xxx.png"``` in *.qml* to refer to the images under the folder.
  
#####  MouseArea
  - ```anchors.fill = XXX``` is mandatory.
  
##### Signals & slots
  - Slots receive the event fired by signals.
  - All the classes which inherit class *QObject* can define signals and slots.
  - Signals and slots are independent, i.e., they don't see each other.
  - Use connection type **excluding** ```Qt::QueuedConnection``` for vector reference type such as ```vector<Mat>&```
  - Check if ```QObject::connect``` succeed:
    + ``` bool isSuccess = (bool) QObject::connect(...)```
    + Note that the correctness of the meta type registration by ```qRegisterMetaType()``` is not guaranteed by this verification.
  - Flows:
    + The signal is emitted.
    + All slots connected to the emitted signal are executed one after another.
    + Execution of the code following the emit statement will occur once all slots have returned. The situation is slightly different when using ```queued connections```; in such a case, the code following the emit keyword will continue immediately, and the slots will be executed later.
  
##### QImage & QPixmap
- Use *QImage* when image processing is necessary. Use *QPixmap* for display.
- Use *QQuickImageProvider* to display the image in *.qml* to take the advantage of independent threads.

##### Thread
- Access the contexted object (by ```context->setContextProperty```) lives in different thread directly from GUI is not allowed, consider access the object from an intermediate c++ class lives in the main GUI thread.
- Get current thread id: ```QThread::currentThreadId```

##### Date type
- Casting between QString and string: 
  + QString -> string: ```qString.toStdString()```
  + string -> QString: ```QString.fromStdString(string object)```

##### ApplicationWindow
 - Remember ```visible:true``` to show the window
 
##### Component
- The first letter of the name of the to-be reused component should be capital. ex: ReuseButton.qml instead of reusedButton.qml
- The file name of the component is the name applied when reused.

##### Appendices
- OpenCV3.1.0 + OpenCV_contrib in .pro
```
INCLUDEPATH += /usr/local/include
INCLUDEPATH += /usr/local/include/opencv2

LIBS += -L/usr/local/lib \
     -lopencv_core \
     -lopencv_imgproc \
     -lopencv_features2d\
     -lopencv_highgui \
     -lopencv_xfeatures2d \
     -lopencv_ccalib \
     -lopencv_calib3d \
     -lopencv_flann \
     -lopencv_ml \
     -lopencv_video \
     -lopencv_imgcodecs \
     ... Add the libraries you need
```

- Pylon5 in .pro
```
INCLUDEPATH += "/Library/Frameworks/pylon.framework/Headers"
DEPENDPATH += "/Library/Frameworks/pylon.framework/Headers"

INCLUDEPATH += "/Library/Frameworks/pylon.framework/Versions/A/Headers"
DEPENDPATH += "/Library/Frameworks/pylon.framework/Versions/A/Headers"

INCLUDEPATH += "/Library/Frameworks/pylon.framework/Headers/GenICam"
DEPENDPATH += "/Library/Frameworks/pylon.framework/Headers/GenICam"

INCLUDEPATH += "/Library/Frameworks/"
DEPENDPATH += "/Library/Frameworks/"

INCLUDEPATH += "/Library/Frameworks/pylon.framework"
LIBS += -F"/Library/Frameworks/" -framework pylon

QMAKE_CXXFLAGS += -F/Library/Frameworks
```







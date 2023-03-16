# Kivy-Pyjnius-Open-URL-Android
Open hyperlink on kivy android app


This instruction contains only bug fix that appears with original pyjnius documentation.<br />
<br />
According to Pyjnius site https://pyjnius.readthedocs.io/en/stable/android.html if you need<br />
to open any website you can use that simple function:<br />
<br />
<br />
<br />
from jnius import cast<br />
from jnius import autoclass<br />
<br />
PythonActivity = autoclass('org.renpy.android.PythonActivity')<br />
Intent = autoclass('android.content.Intent')<br />
Uri = autoclass('android.net.Uri')<br />
<br />
intent = Intent()<br />
intent.setAction(Intent.ACTION_VIEW)<br />
intent.setData(Uri.parse('http://kivy.org'))<br />
<br />
currentActivity = cast('android.app.Activity', PythonActivity.mActivity)<br />
currentActivity.startActivity(intent)<br />
<br />
<br />
<br />
Unfortunately this won't work. Traceback from logcat will look like this:<br />
<br />
"jnius.JavaException: Class not found 'org/renpy/android/PythonActivity'"<br />
<br />
That is because jnius will search for path 'org/renpy/android/PythonActivity' that does not exist. <br />
Default path for PythonActivity is set in buildozer.spec file as :<br />
<br />
###################<br />
#android.entrypoint = org.kivy.android.PythonActivity<br />
###################<br />
<br />
So if you want to open website all you have to change in code above is this line :<br />
<br />
PythonActivity = autoclass('org.kivy.android.PythonActivity')<br />
<br />
####################<br />
<br />
This is the right code:<br />
########################<br />
<br />
<br />
PythonActivity = autoclass('org.kivy.android.PythonActivity')<br />
Intent = autoclass('android.content.Intent')<br />
Uri = autoclass('android.net.Uri')<br />
<br />
intent = Intent()<br />
intent.setAction(Intent.ACTION_VIEW)<br />
intent.setData(Uri.parse('http://kivy.org'))<br />
<br />
currentActivity = cast('android.app.Activity', PythonActivity.mActivity)<br />
currentActivity.startActivity(intent)<br />
<br />
######################<br />
<br />
Do not forget to write "pyjnius" to requirements in buildozer.spec file<br />

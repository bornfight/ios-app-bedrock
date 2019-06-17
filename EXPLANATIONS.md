## Environment Variables

What?

Variables located in the system building/running the application, depending on the use case.


Why?

Same reasoning as using any other variables in any other programming language - to separate code from data.


Which ones do we use?

The ones provided by Fastlane, and any custom ones as deemed necessary.
To find out which environment variables a Fastlane action provides, run `fastlane action $ACTION_NAME` in your Terminal.


How do I find out which one I need?

Most of the needed environment variables should already be in the predefined environment files. 
If you need to add another one, simply add it to an `.env` file.

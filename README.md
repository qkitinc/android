# android

Step 1 Generate a Signed Release Key file
keytool -genkey -v -keystore demo.keystore -alias demo -keyalg RSA -keysize 2048 -validity 10000

Step 2 Setting up Gradle variables
MYAPP_RELEASE_STORE_FILE=demo.keystore
MYAPP_RELEASE_KEY_ALIAS=demo
MYAPP_RELEASE_STORE_PASSWORD=demo*123#
MYAPP_RELEASE_KEY_PASSWORD=demo*123#

Step 3 Adding signing config to app's Gradle config
signingConfigs
    {
        release
        {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE'))
            {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }

buildTypes 
{
        release 
 {
 
            signingConfig signingConfigs.release
        }
}

Step 4 Generating the APK

./gradlew assembleRelease

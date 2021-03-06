# Biometric-Compat

It provides an easy way to implement fingerprint authentication without having to deal with all the boilerplate stuff going on inside. It is also compatible from Android M to Android P.

<img src="https://img.shields.io/badge/API-23%2B-blue.svg?style=flat" style="max-width:100%;" alt="API" data-canonical-src="https://img.shields.io/badge/API-23%2B-blue.svg?style=flat" style="max-width:100%;">       <img src="https://img.shields.io/badge/version-0.7.1-green.svg?style=flat" style="max-width:100%;" alt="version" data-canonical-src="https://img.shields.io/badge/version-0.7.1-green.svg?style=flat" style="max-width:100%;">



<p><a href="https://github.com/nirav-tukadiya/Biometric-Compat/blob/master/media/1.png" target="_blank"><img src="https://github.com/nirav-tukadiya/Biometric-Compat/blob/master/media/1.png" width="250" style="max-width:100%;"></a></p>
</br></br></br>




<b>Gradle Dependecy</b></br>

```gradle

repositories {
        jcenter()
        maven {
             url "https://dl.bintray.com/nirav-tukadiya/maven/"
        }
}

dependencies {
        implementation 'com.niravtukadiya.compat.biometric:biometric-compat:0.9.0'
}
```

<h2>Usage</h2>

```

 BiometricCompat.BiometricBuilder(context)
                    .setTitle("Add a title")
                    .setSubtitle("Add a subtitle")
                    .setDescription("Add a description")
                    .setLayout(R.layout.your_layout_resource)
                    .setNegativeButtonText("Add a cancel button")
                    .build()
                    .authenticate(biometricCallback)

```

Note: in case of custom view, it shall have following children:
```
 bc_btn_cancel: Button
 bc_item_title: TextView
 bc_item_status: TextView
 bc_item_subtitle: TextView
 bc_item_description: TextView
 bc_img_logo: ImageView
```

The ```BiometricCallback``` class has the following callback methods:

```
    // one of the pre conditions failed
    // ON_SDK_NOT_SUPPORTED - minimum sdk version required is Build.VERSION_CODES.M
    // ON_BIOMETRIC_AUTH_NOT_SUPPORTED - hardware isn't present
    // ON_BIOMETRIC_AUTH_NOT_AVAILABLE - no fingerprints are enrolled
    // ON_BIOMETRIC_AUTH_PERMISSION_NOT_GRANTED - USE_FINGERPRINT permission is not granted
    fun onPreConditionsFailed(error: BiometricError)

    // when title, subtitle, description or the negative button text is empty
    fun onBiometricAuthenticationInternalError(error: String?)

    //Called when a biometric is valid but not recognized.
    fun onAuthenticationFailed()

    //when user cancels authentication
    fun onAuthenticationCancelled()

    //Called when a biometric is recognized.
    fun onAuthenticationSuccessful()

    //when a recoverable error has been encountered during authentication.
    fun onAuthenticationHelp(helpCode: Int, helpString: CharSequence?)

    //Called when an unrecoverable error has been encountered and the operation is complete
    fun onAuthenticationError(errorCode: Int, errString: CharSequence?)
```

Please refer to [Help and Error Codes](https://developer.android.com/reference/android/hardware/biometrics/BiometricPrompt#constants_1) of BiometricPrompt


Acknowledgements
----------------

[Biometric-Auth-Sample](https://github.com/anitaa1990/Biometric-Auth-Sample) by Anitaa Murthy


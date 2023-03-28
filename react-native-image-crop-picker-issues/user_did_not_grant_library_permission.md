## Problem
To use cropper tool from `react-native-image-crop-picker` we can use the following: 
```
 ImagePicker.openCropper({...})
 
 ```
 This will work fine if you use it after using ImagePicker.openCamera({...}) but if you want to use it only as a cropper this will not work and will throw error: 
 
 `User did not grant library permission` 

 even if you have these permissions in AndroidManifest which is required for using cropper.

 ```
  WRITE_EXTERNAL_STORAGE
  READ_EXTERNAL_STORAGE
```

and even when you are explicitly requesting permission from user before using the cropper.

![image](https://user-images.githubusercontent.com/11868557/228209902-79b73543-074a-4a69-9cda-94891b0a659f.png)


## Environment
- OS: `Android`
- React Native: `^0.70.6`
- react-native-image-crop-picker: `^0.39.0`

## How you fix it
Currently there are not proper fix so we need to make some changes to the library and make a patch. To make a patch you will need `patch-package` npm package. you can check it here: [Learn more about patch-package](https://www.npmjs.com/package/patch-package). 

## Solution
###### Following these instructions to make the changes in the library:
- Go to `node_modules/react-native-image-crop-picker/android/src/main/java/com/reactnative/ivpusic/imagepicker/PickerModule.java`
- In the `openCropper` function remove the permissionCheck fuction and only leave `startCropping()`

```
  @ReactMethod
  public void openCropper(final ReadableMap options, final Promise promise) {
    final Activity activity = getCurrentActivity();

    if (activity == null) {
        promise.reject(E_ACTIVITY_DOES_NOT_EXIST, "Activity doesn't exist");
        return;
    }

    setConfiguration(options);
    resultCollector.setup(promise, false);

    final Uri uri = Uri.parse(options.getString("path"));
    startCropping(activity, uri);
  }
```

<img width="1004" alt="image" src="https://user-images.githubusercontent.com/11868557/228209731-58f66049-b622-48c2-a8a3-a32b72a31d4c.png">

# LAB: Console and Cloud Shell

## Objectives
In this lab, you learn how to perform the following tasks:

    1. Get access to Google Cloud.
    2. Create a Cloud Storage bucket using the Cloud Console.
    3. Create a Cloud Storage bucket using Cloud Shell.
    4. Become familiar with Cloud Shell features.

## Steps
1. Create a Cloud Storage bucket using the Cloud Console.
  - Create Bucket

        gsutil mb gs://bkt1

  - List Buckets in your Project
  
        gsutil ls
        
2.  Create a Cloud Storage bucket using the Cloud Shell.
  - Create Bucket

        gsutil mb gs://bkt2

  - List Buckets in your Project
  
        gsutil ls
3. Become familiar with Cloud Shell features.
_Explore more Cloud Shell features_

  - Upload a file
  
      Open Cloud Shell
      
      Click the three dots icon in the Cloud Shell toolbar to display further options.

      Click Upload file. Upload any file from your local machine to the Cloud Shell VM. This file will be referred to as [MY_FILE].

      Confirm that the file was uploaded.
      
            ls
            
      Copy the file into one of the buckets you created earlier in the lab
      
            gsutil cp [MY_FILE] gs://[BUCKET_NAME]
 
 _Create a persistent state in Cloud Shell_
 
  - Identify available regions
     
     To list available regions, execute the following command:

            gcloud compute regions list

     Select a region from the list and note the value in any text editor. This region will now be referred to as [YOUR_REGION] in the remainder of the lab

 - Create and verify an environment variable

     Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:

            INFRACLASS_REGION=[YOUR_REGION]

     Verify it with echo:

            echo $INFRACLASS_REGION
  
 - Append the environment variable to a file
 
     Create a subdirectory for materials used in this class:

            mkdir infraclass

     Create a file called config in the infraclass directory:

            touch infraclass/config

    Append the value of your Region environment variable to the config file:

            echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config

    Create a second environment variable for your Project ID, replacing [YOUR_PROJECT_ID] with your Project ID. You can find the project ID on the Cloud Console Home page.

             INFRACLASS_PROJECT_ID=[YOUR_PROJECT_ID]

    Append the value of your Project ID environment variable to the config file:

            echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config

    Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:

            source infraclass/config
            
            echo $INFRACLASS_PROJECT_ID
    Close and re-open Cloud Shell. Then issue the echo command again:

            echo $INFRACLASS_PROJECT_ID

 There will be no output because the environment variable no longer exists.

 - Modify the bash profile and create persistence
 
    Edit the shell profile with the following command:

            nano .profile

  Add the following line to the end of the file:

            source infraclass/config
  
 Press Ctrl+O, ENTER to save the file, and then press Ctrl+X to exit nano.

 Close and then re-open Cloud Shell to cycle the VM.

 Use the echo command to verify that the variable is still set:

          echo $INFRACLASS_PROJECT_ID

You should now see the expected value that you set in the config file.

+++
date = "2017-10-26T08:44:39-07:00"
title = "Where in the World is Andor Tutorial"
slug = ""
comments = false
showpagemeta = true
categories = []
tags = []
draft = false
showcomments = true

+++

I haven't used AWS that much, so I wanted to follow `https://aws.amazon.com/serverless/build-a-web-app/` as much as possible. 

There are few high level concepts that are trying to achieve to make the app to work. 
    
    - The phone needs to send my location to an endpoint.
    - The endpoint needs to have an public 

1. Create a AWS S3 Bucket.
    a. Create your bucket policy and add it to the bucket
    b. Sync files on the UI
    c. Host website 

      ```

      BUCKET_NAME={YOUR_BUCKET_NAME_HERE}
      aws s3 mb s3://${BUCKET_NAME} --region us-east-1 #change region if you want

      echo "Creating Bucket Policy"
      echo "Warning! This is a open access policy for the user."
      echo "{
   	    "Version": "2012-10-17",
    	"Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::sampleserverlessapp/*"
        }
    	]
		}" > policy.json

	   echo "Adding bucket policy"	
       aws s3api put-bucket-policy  --bucket s3://${BUCKET_NAME} --policy file://policy.json

       echo "Sync Files for UI"
       aws s3 sync s3://{TODO} s3://{BUCKET_NAME} --region us-east-1

       echo "Host Website"
       aws s3 website s3://{BUCKET_NAME} --index-document index.html  --error-document error.html
      ```


2. Use AWS's Cognito tool to create users

This was a little weird. As a quick disclaimer, I relied pretty heavily on AWS's cognito tool. I've never used it before and I was curious how it worked. 


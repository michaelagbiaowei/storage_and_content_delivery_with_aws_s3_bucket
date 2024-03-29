## **Deploy Static Website on AWS Using Amazon S3 Bucket and Content Delivery Network (CloudFront)**

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">Project Overview</a>
      <ul>
        <li><a href="#prerequisites">What are S3 Buckets</a></li>
        <li><a href="#built-with">AWS S3 Basics</a></li>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#built-with">Frameworks</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#steps">Create S3 Bucket</a></li>
        <li><a href="#steps">General configuration</a></li>
        <li><a href="#steps">Public Access settings</a></li>
        <li><a href="#steps">Bucket Versioning and Encryption</a></li>
        <li><a href="#steps">Upload File/Folders to the Bucket</a></li>
        <li><a href="#steps">Secure Bucket via IAM</a></li>
        <li><a href="#steps">Enable Static Website Hosting</a></li>
        <li><a href="#steps">Create Distribution</a></li>
        <li><a href="#steps">Access Website in Web Browser</a></li>
      </ul>
    </li>
    <li><a href="#contact">Contacts</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## Project Overview

## What are Amazon S3 Buckets?

S3 stands for Simple Storage Service and a Bucket is a resource that is being provided and offered by the Amazon S3 service.

Buckets consists of data and it's meta data, the data can be any static file e.g., .pdf, png, .txt and many more.

This service enables organizations of all sizes and across various industries to store large amounts of data for a variety of use cases including websites, mobile applications, disaster recovery, and big data analytics.

## AWS S3 Basics

Amazon leverages a flat, non-hierarchical structure, storing data as objects within buckets. Below are some of the most important basic concepts of S3.

- **Buckets** serve as the containers for objects and provide the mechanisms necessary to control access to them

- **An object** is not only the file that is being uploaded but can also include the metadata attributes that describe the file

- **Access points** are named network endpoints that are attached to buckets that can be used to perform S3 object operations. Each access points have distinct permissions and network controls that are applied to any request made through that access point.

- **Bucket Policies** provide granular controls to buckets and the objects stored within buckets.

- **Access Control Lists** vary from policies in that they can add grant permissions on buckets or on individual objects

- **AWS Identity and Access Management** provides additional management of how users can access S3 resources

## What is a CDN?

A CDN or Content Delivery Network – is a global network of servers that work together to provide ultra-fast delivery of Internet content, such as web pages, static objects, videos etc.

When people try to access content via the Internet, a CDN makes sure they get it delivered from servers nearest to them, so it arrives faster.

**Simple example:** Doe and Jane both listened the same latest Music. While Doe's Music is delivered from a datacenter in South Africa, because that’s where he resides, Jane's Music is delivered from a datacenter in Kenya, because that’s where she lives. This is made possible through CDN.

**Amazon CloudFront** is the web service to use when seeking to speed up the distribution of your objects, either in dynamic or static files through a worldwide network of data centers referred to as edge locations.

Content that is served by CloudFront is delivered with the best performance possible, meaning higher speed of delivery.

<img align= "center" alt="Coding" src="https://isotropic.co/wp-content/uploads/2022/04/CF-Cache.png">

## TASKS

The cloud is perfect for hosting static websites that only include HTML, CSS, and JavaScript files that require no server-side processing. The whole project has two major intentions to implement:

- Hosting a static website on S3 and
- Accessing the cached website pages using CloudFront content delivery network (CDN) service. Recall that CloudFront offers low latency and high transfer speeds during website rendering.

Note that Static website hosting essentially requires a public bucket, whereas the CloudFront can work with public and private buckets.

In this project, you will deploy a static website to AWS by performing the following steps:

1. You will create a public S3 bucket and upload the website files to your bucket.
2. You will configure the bucket for website hosting and secure it using IAM policies.
3. You will speed up content delivery using AWS’s content distribution network service, CloudFront.
4. You will access your website in a browser using the unique CloudFront endpoint.

## Getting Started

## Prerequisite

- Amazon Account
- An **udacity-starter-website** codebase on local machine

## Student-ready starter code Frameworks and Languages

<img src="https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E" />

<img src="https://img.shields.io/badge/Jquery-323330?style=for-the-badge&logo=Jquery&logoColor=F7DF1E" /> 

![Node.js](https://img.shields.io/badge/Node.js-%234ea94b.svg?style=for-the-badge&logo=node.js&logoColor=white)

<img src="https://img.shields.io/badge/Jquery-323330?style=for-the-badge&logo=Jquery&logoColor=F7DF1E" /> 

![Bootstrap](https://img.shields.io/badge/Bootstrap-%230175C2.svg?style=for-the-badge&logo=Bootstrap&logoColor=white) 

<img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" /> 

<img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" /> 

## 1. Create a Bucket

Navigate to the S3 dashboard, and click on the Create bucket button. It will launch a new wizard

![s1](/images/s1.png)

We create a bucket first, and later we upload files and folders to it.

## 2. General configuration

Provide the bucket-name. The bucket name must be unique worldwide e.g. demo-bucket-2022-12-09, and must not contain spaces or uppercase letters.

![s1](images/s2.png)

## 3. Public Access settings

## What is Public Access in S3

The key to most if not all of the security breaches within S3 buckets is due to the public access configurations set on the buckets or objects. Allowing public access allows access to virtually anyone in the entire world, granted they have the unique ARN of the specific bucket or object.

As shown in the snapshot below, there are four basic options available to limit public access within your account.

- **Block public access to buckets and objects granted through new access control lists (ACLs):** This setting will prevent the creation of new ACLS that permit public access, without impacting existing buckets.

- **Block public access to buckets and objects granted through any access control lists (ACLs):** This setting will prevent the creation of new ACLS that permit public access and will override existing bucket ACLs that permit public access.

- **Block public access to buckets and objects granted through new public bucket or access point policies:** This setting will prevent the creation of future IAM policies that permit public access, without impacting existing buckets.

- **Block public and cross-account access to buckets and objects through anybucket or access point policies:** This setting will prevent the creation of future IAM policies that permit public access and will override existing policies that permit public access.

Allow all public access.

![s1](/images/s3.png)

## 4. Bucket Versioning and Encryption

- Bucket Versioning - Keep it disabled.

- Encryption - If enabled, it will encrypt the files being stored in the bucket.

- Object Lock - If enables, it will prevent the files in the bucket from being deleted or modified

![s1](/images/s4.png)

The snapshot below shows that the bucket is in the Region: US East (N. Virginia) us-east-1, and it has a unique Amazon resource name (ARN): **arn:aws:s3:::my-400894577556-bucket/index.html**. You can view more details of the bucket.

![s1](/images/n1.png)

## 5. Upload File/Folders to the Bucket

In the snapshots above, we have created a public bucket. Let's see how to upload files and
folders to the bucket, and configure additional settings.

Click on the Upload button to upload files and folders into the current bucket. In the snapshot below, I have uploaded a the required file and directories.

![s1](/images/s6.png)

![s1](/images/s7.png)

![s1](/images/s8.png)

## 6. Secure Bucket via IAM

Click on the “Permissions” tab.

![s1](/images/s9a.png)

Edith the bucket policy as shown below

![s1](/images/s9.png)

## 7. Enable Static Website Hosting

Click on your bucket properties

![s1](/images/s10.png)

Scroll down to the bottom page and click on Edit icon

![s1](/images/s11.png)

In the index document, write the name of your uploaded html file and click on **save changes**

![s1](/images/s12.png)

When our S3 Bucket is Enabled, We can test our endpoint using the Bucket Website Endpoint url as shown on the images below

![s1](/images/e1.png)

## 8. Create Distribution

![s1](/images/c1.png)

Now we will create CloudFront Distribution for our bucket. Currently, we do not have any distributions. We will click on Create Distribution.

![s1](/images/c2.png)

Here we will provide the Origin domain which in our case is from Amazon S3 i.e. **[my-400894577556-bucket.s3.amazonaws.com](https://my-400894577556-bucket.s3.amazonaws.com/index.html)**. Note that an origin is a location where content is stored, and from which CloudFront gets content to serve to viewers.

In S3 bucket access, we will select **Bucket must allow public access**

![s1](/images/c3.png)

Redirect all HTTP request to HTTPS

![s1](/images/c4.png)

![s1](/images/c5.png)

After these steps are taken, users can only access our files through CloudFront, and also directly from the S3 bucket.

In the **Default root object**, we will write the name of the file i.e. index.html that we uploaded to our bucket.

![s1](/images/c6.png)

Now after creating our distribution we can view our newly created OAI.

![s1](/images/c7.png)

**Note** Remember, as soon as your CloudFront distribution is Deployed, it attaches to S3 and starts caching the S3 private pages. Once the caching is complete, the CloudFront domain name URL will stop redirecting to the S3 object URL. CloudFront may take 10-30 minutes (or more) to cache the S3 page, and you will be able to view the webpage, as shown below.

Now to check whether things are working properly let's test our CloudFront Distribution. We will copy the Distribution domain name **[https://dvhvfum3rmz3k.cloudfront.net](https://dvhvfum3rmz3k.cloudfront.net)**. and enter it into our browser.

![s1](/images/c8.png)

## **Access Website in Web Browser**

1.  Our CloudFront Distribution is working perfectly fine. We have successfully learned that how to use CloudFront with S3.

**[https://dvhvfum3rmz3k.cloudfront.net](https://dvhvfum3rmz3k.cloudfront.net)**

![s1](/images/f1.png)

2. Access the website via website-endpoint.

**[http://my-400894577556-bucket.s3-website-us-east-1.amazonaws.com/](http://my-400894577556-bucket.s3-website-us-east-1.amazonaws.com/)**

![s1](/images/f3.png)

3. Access the bucket object via its S3 object URL.

**[https://my-400894577556-bucket.s3.amazonaws.com/index.html](https://my-400894577556-bucket.s3.amazonaws.com/index.html)**

![s1](/images/f2.png)

## 🔗 Contacts

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/maiempire/)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/2348089440108)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=Twitter&logoColor=white)](https://twitter.com/michaelagbiaow2)

## Acknowledgments

- [Amazon S3 Access Control - IAM Policies, Bucket Policies and ACLs](https://www.youtube.com/watch?v=xFzJw6wJ8eY)
- [Udacity Cloud DevOps Nanodegree Program](udacity.com)
- [ALX Africa](https://www.alxafrica.com/)

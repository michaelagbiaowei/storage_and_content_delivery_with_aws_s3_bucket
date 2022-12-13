## **Deploy Static Website on AWS**

## Project Overview

The cloud is perfect for hosting static websites that only include HTML, CSS, and JavaScript files that require no server-side processing. The whole project has two major intentions to implement:

- Hosting a static website on S3 and
- Accessing the cached website pages using CloudFront content delivery network (CDN) service. Recall that CloudFront offers low latency and high transfer speeds during website rendering.

              *Note that Static website hosting essentially requires a public bucket, whereas the CloudFront can work with public and private buckets*.

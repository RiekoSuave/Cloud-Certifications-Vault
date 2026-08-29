See also: [[S3]]

See also: [[S3 Security]]

## What Problem Does It Solve?

Allows static website content to be hosted directly from an S3 bucket.

This provides a simple way to make static web content accessible over the Internet.

---

## Type

Static Website Hosting

---

## What Is S3 Static Website Hosting?

S3 can host static websites.

A static website contains files such as:

- HTML
- CSS
- JavaScript
- Images

The website files are stored as objects inside an S3 bucket.

### Memory Trick

S3 = Store Website Files

---

## Basic Architecture

User

↓

Internet

↓

S3 Website Endpoint

↓

S3 Bucket

↓

Static Website Files

---

## Static Content

S3 website hosting is designed for:

Static content

Examples:

- HTML pages
- CSS
- JavaScript
- Images
- Other static files

---

## Website Endpoint

When static website hosting is enabled, S3 provides a website endpoint.

Your course notes show that the exact URL format depends on the AWS Region.

### Memory Trick

Enable Website Hosting

↓

Get Website Endpoint

---

## Public Access

If the website needs to be publicly accessible over the Internet, the required public read permissions must be configured.

This relates directly to:

[[S3 Security]]

---

## Bucket Policy

A Bucket Policy can be used to allow the required public access to the website content.

### Important

S3 also has:

Block Public Access

settings.

These settings must be considered when intentionally configuring a public S3 website.

---

## 403 Forbidden

Your course specifically calls out:

403 Forbidden

If you receive this error when trying to access an S3-hosted website, check whether the:

Bucket Policy allows public reads.

### Memory Trick

S3 Website + 403

→ Check Bucket Policy

---

## Common Use Cases

- Simple static websites
- Portfolio sites
- Documentation sites
- Static web content

---

## S3 Website vs Traditional Web Server

### S3

Stores and serves static website files.

### EC2

Can run a traditional web server and application software.

| S3 Website | EC2 |
|---|---|
| Static content | Can run server software |
| No server management | Server management |
| Object storage | Virtual machine |

---

## Security Connection

Public S3 website access is an intentional security configuration.

Remember the relationship:

S3 Website

↓

Needs Public Read Access

↓

Bucket Policy

↓

Block Public Access Settings Must Be Considered

See:

[[S3 Security]]

---

## Exam Scenarios

A company wants to host a simple static website using files stored in S3.

→ S3 Static Website Hosting

---

A static S3 website returns:

403 Forbidden

What should you check?

→ Make sure the Bucket Policy allows public reads

---

A website requires server-side application processing.

→ Static S3 website hosting alone is not designed for that workload

---

## Exam Keywords

Static website

S3

Website endpoint

Public access

Bucket Policy

403 Forbidden

---

## Memory Tricks

S3 Website = Static Content

Static = HTML + CSS + JavaScript + Images

403 = Check Bucket Policy
## Introduction to Progressive Web Applications | Part-1

# WHAT WE ARE GOING TO LEARN ?

1.  What is a Progressive Web App (PWA)?
2. Native vs. Web Apps vs. PWA
3. Advantages and benefits of using a PWA
4. Technical components of a PWA
5. How to convert basic Angular app to a PWA (Part 2)


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611575135286/MJlJu3i6H.png)

--------------------------------------------------------------------------

## 1.  What is a Progressive Web App (PWA)?

-  A progressive web app is a website that **functions just like a native app**. It has all the functionality of a native app and still manages to deliver the usability of a website. 
- In order for a website to perform well and index on top, there are some checklists of Google, like page speed, mobile friendliness, response time, etc. PWAs are created for fulfilling the majority of requirements listed in Google's checklist. So at the end, a PWA is **fast, reliable and engaging**.
- PWAs are intended to address a variety of problems ranging from inadequate networks to data obstruction or total lack of connectivity. By allowing websites to load even when there is no **network connection**.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611575357003/lpBXm5cNm.png)

- **Reliable** – Load instantly and never show the “No Internet Connection” page, even in uncertain network conditions.
- **Fast** – Respond quickly to user interactions with silky smooth animations and no janky scrolling.
- **Engaging** – Feel like a natural app on the device, with an immersive user experience.

**We will dive deep into this in the later part of the tutorial.**

--------------------------------------------------------------------------

## 2. Native vs. Web Apps vs. PWA

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611575881918/e-KSrqVd5.png)

- **Native Apps** have more capabilities like **working offline, quick loading speeds**. etc.
- **Web Apps** have more reach, once a web app went online it is easy to allow more users to use it.
- **PWAs** offer the **best of both worlds**. They are the online counterparts of native mobile apps that can run offline, send push notifications, and load with lightning speeds. They can be developed faster than native or web apps and deployed instantly.
- PWAs make it easy for developers to deploy and maintain the app and simultaneously it also seamlessly allows users to access all the features of a native app.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611575940695/CxMPQvTSM.png)


You can see the comparison between Progressive Web Apps and a Native Applications.

--------------------------------------------------------------------------

## 3. Advantages and Benefits of using a PWA

We can also say, `Why should you build a Progressive Web App?`

**To answer that** - 


> 
There are several reasons why we have to go with Progressive Web Apps. 

**We will discuss some of them now:**

### **A. Quick Response to Users** 

PWAs are highly responsive and compatible with every device since they adjust the layout according to the device.  PWA offers smooth scrolling and also provides fast response when a user interacts with it.

### **B. Reliable Despite Network flaws**

According to studies, more than 65% of the world makes use of a 2G internet connection. So, even when the network is slow, we can rely on Progressive Web Apps, as it can function offline.  A PWA immediately loads data from cache and runs seamlessly on both 2G and 3G network conditions.

### **C. Secure **

PWAs are safer than normal web apps, since they are always served via HTTPS instead of HTTP. 

### **D. Easy Installation**

Installing a native mobile app requires more data, more time. But PWA is 90% lower in size which makes it extremely easy to install and use all the services. Also PWA consumes less mobile data, mobile battery.


### **E. Easy Updates**

Since no app store act as a mediator, users can take advantage of the updated version as soon as you update it from developer end. There is no requirement of any app store, user can have updated features with a simple refresh of the application.


### **F. Lightweight**

PWAs are extremely lightweight. To give an example, when compared to the native mobile app, the Twitter Lite PWA is only 600KB whereas the native Android app requires about 25MB for download and the native iOS app is about 215MB in size.


### **G. High Performance Website**

Poor website loading is a common issue.  53% of users abandon a website if it is too slow. Using PWAs, the performance of a website can be significantly improved.

### **H. Feels like a Native App**

It is hard to find a difference between a PWA and a native app. A PWA exactly looks and feels like a native app and even provides similar features such as push notification, physical installation, display icon on the home screen, etc. It enables users to engage much like a native app. 


--------------------------------------------------------------------------


## 4. Technical components of a PWA

In order to convert a normal app to a Progressive Web App, there are few steps that we have to follow or few configurations that we have to do to our application. And remember one thing, converting applications to PWA does not depend on kind of language we use to develop that application. 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611576997207/elQd6gRi2.png)

These components are a prerequisite to develop a successful PWA:
1. Service worker
2. Web App Manifest and 
3. HTTPS

Lets try to understand about each of them,

### 1. Service Worker


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611577123567/c6Ir3wTIA.png)

This is how Javascript typically behaves, it runs in a single thread, that means our entire web application which consists of multiple pages or if we are using angular, it is a single page, runs on a single thread.

Javascript and browser allows us to run another thread, which is called as a service worker. This is one of the main thread, but a different thread than our JavaScript code. As you can see in the picture. This service worker thread is decoupled with your application, but still can do different operations like caching the files, sending push notifications, and interacting with the API calls from an application. For example, our application has an GET API call, this service worker can save that data and cache it locally. Therefore, that it can allow our app to work offline as well.


### 2. Web App Manifest

The purpose of the app manifest file is to define the resources that our app needs. It includes the icons, your app’s displayed name, background color, theme, and other necessary details that transform the website into an app-like format. 

### 3. HTTPS

Service Workers can intercept network requests and modify responses. They know all actions on the customer side, so Progressive Web App must be served over a secure network. Most of the features related to a PWA such as geolocation and even service workers are available only once the app has been loaded using HTTPS.


--------------------------------------------------------------------------

## 5. How to convert basic Angular app to a PWA

We will discuss more about how to convert basic Angular app to a PWA with code examples in the next part of this tutorial.

The URL for the next part is: 

 
> 
[**Introduction to Progressive Web Applications (Angular), a Practical Approach| Part-2**](https://charandev.com/introduction-to-progressive-web-applications-angular-a-practical-approachor-part-2) 


--------------------------------------------------------------------------

Hopefully, you have learned some basics about Progressive Web Apps.
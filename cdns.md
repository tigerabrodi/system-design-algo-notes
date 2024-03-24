# The problem

Say you have your origin server in the US and you have users in Europe. When a user in Europe tries to access your website, the request has to travel all the way to the US and back. This can cause latency and slow down your website.

This is where CDNs come in.

# The solution

A CDN is a network of servers distributed across the globe. You can only cache static assets like images, CSS, and JavaScript files on a CDN. When a user in Europe tries to access your website, the request is routed to the nearest server in the CDN. This reduces latency and speeds up your website.

You can't run code on CDNs. They are only used to cache static assets. If you need to run code close to your users, you can use edge computing services like Cloudflare Workers.

# Pull CDNs vs Push CDNs

## Pull CDNs

In a pull CDN, the CDN server will fetch the content from your origin server the first time a user requests it. The CDN server will then cache the content and serve it to subsequent users.

For example, if a user in Europe tries to access your website in the US, the request will be routed to the nearest CDN server. The CDN server will then fetch the content from your origin server and cache it. The next time a user in Europe tries to access your website, the content will be served from the CDN server instead of the origin server.

## Push CDNs

In a push CDN, the origin server pushes the content to the CDN servers. This is useful when you have a large number of users accessing the same content because the content would be pushed to all CDN servers.

For example, if a user uploads a video to YouTube, the video will first be uploaded to the origin server. The origin server will then push the video to the CDN servers. This way, when a user tries to access the video, it is served from the CDN servers instead of the origin server.

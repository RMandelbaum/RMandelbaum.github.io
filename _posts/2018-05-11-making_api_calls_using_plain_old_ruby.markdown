---
layout: post
title:      "Making API Calls Using Plain Old Ruby"
date:       2018-05-12 01:49:37 +0000
permalink:  making_api_calls_using_plain_old_ruby
---


For one of my code challenges, I was tasked to make an API call using Ruby. I was only familiar with making API calls using JavaScript with `fetch` or `get`, so I had to do some research for the solution. 

Rails has specific conventions to send API requests and receive information in a RESTful manner, but this challenge was in plain old Ruby. So, my search for an answer continued. After playing around with a few options, I landed on these lines of code that I wanted to share with anyone facing a similar challenge. 

```
uri = URI.parse("http://[example-url].json?id=?&page=?")
http = Net::HTTP.new(uri.host, uri.port)
request = Net::HTTP::Get.new(uri.request_uri)
response = http.request(request)
result = JSON.parse(response.body)
```

And that’s pretty much it. Always add a `binding.pry` or `byebug` to ensure the information is correct, and you’ll be set to play around with your API data. 


# Davids Website

A personal website telling the world about me, my interests, and career goals. To visit the deployed version, go to www.davidcharlesgoldstein.com.

![screenshot](screenshots/1.png)

## Getting Started

The project is built using the R library [blogdown](https://bookdown.org/yihui/blogdown/). It's a simple tool which allows you to serve and deploy sites using [R markdown](http://rmarkdown.rstudio.com/), a language usually meant for displaying graphs and trend analysis, but suprisingly useful for organizing single page applications.

### Prerequisites

1. [Download R Studio](https://www.rstudio.com/products/rstudio/download/). Not a direct dependency, but makes provides a nice interface for installing R and running R commands.

### Installing

```sh
git clone https://github.com/dgoldstein1/DavidsWebsite.git
```

Open up the directory in R Studio and run the following :

```r
# Install blogdown
install.packages("blogdown")
# install hugo
blogdown::install_hugo()
# serve the site
blogdown::serve_site()
```

R studio should output that the site is successfully running : 

```r
Started building sites ...

Built site for language en:
0 draft content
0 future content
0 expired content
5 regular pages created
6 other pages created
0 non-page files copied
0 paginator pages created
0 tags created
0 categories created
total in 10 ms
Serving the directory {your curr dir}/DavidsWebsite at http://127.0.0.1:4321
```

Open up `http://127.0.0.1:4321` in your browser and you should be taken to the website.

### Website Metrics

This website provides live metrics when the page loads by making requests to get the current user's ip address and then post it to [a backend server I wrote which keeps track of website visits](https://github.com/dgoldstein1/websiteAnalytics-backend). The request javascript code is found in `config.toml` :

```js
// send out requests
  let proxy="https://cors-anywhere.herokuapp.com/"
  let geoIpServer="http://freegeoip.net/json"
  let metricsServer="https://quiet-brushlands-26130.herokuapp.com/visits"
  let localinstance="http://localhost:5000/visits"

  // get IP information and send to analytics database
  $.getJSON(proxy + geoIpServer, function(ipResponse){
    console.log("current ipResponse", ipResponse)
    if (ipResponse) {
      // formulate request to metrics server      
      $.post(metricsServer, JSON.stringify(ipResponse), function(res) {
        console.log("response from db",res)
      })
    }
  });
```

Feel free to change the location of the urls if you want to deploy your own metrics server.

## Deployment

Blogdown generates static html in the `/public` folder and there are multiple ways to deploy this. See [this guide](https://bookdown.org/yihui/blogdown/deployment.html) for more information. Currently, www.davidcharlesgoldstein.com is deployed through [netifly](app.netlify.com). To redeploy, simply merge or push changes to `master.`

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **David Goldstein** - [Decipher Technology Studios](deciphernow.com) - [Personal Website](http://www.davidcharlesgoldstein.com/?github-davids-website)
## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details


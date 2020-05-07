
### post

To make a post
* create a `_posts/<post>.md` file
* add the appropriate headers that the other posts have 
* commit/push, wait like 2m to see it live

### resume

To make a resume change
* run `make` to setup the resume docker container
* modify resume.json
* run make serve and visit `mike.jaqobi.com:9000/resume.pdf` to see it
* once ok with it, from HTML, right click, print, print to pdf
* scp the pdf to `<dev.jaqobi.com:9000/resume.html>/resume/resume.pdf`
* commit/push, wait like 2m to see it live

troubleshooting
* make sure port 9000 is open
* make sure you actually ran `make build`

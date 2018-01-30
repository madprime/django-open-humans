# Open Humans Uploader
*it's like Jekyll for Open Humans* or something along the lines.

Ultimately this should be an easy to deploy Django project that functions as a
file uploader for individual *Open Humans* projects. It should be easy deploy to
*heroku* and the configuration/styling of the project website should be done more
or less exclusively through a `yaml` configuration file and `markdown` files that
are rendered to HTML.

## Configuration

### Setting up a project on *Open Humans*
To connect this data uploader to your own *Open Humans* project you should start out by
[creating a new project on Open Humans](https://www.openhumans.org/direct-sharing/projects/manage/).
Select the *Create a new OAuth2 data request project* button and fill out the form.

For this uploader to work you have to give the correct redirect URL in the form (it's the last field).
Our uploader expects redirects to `youraddress.com/complete`. If you run this tool on your development
machine it will probably be `http://127.0.0.1:5000/complete`. If you deploy it to *heroku* it will be
`https://yourappname.herokuapp.com/complete`.

### Configure the *Open Humans Uploader*

This configuration is done by two means:
1. The `config.yaml` file contains information that will be displayed on your website later on. As such it is not sensitive and can be publicly available.
2. For sensitive information there is the `.env` file that contains your **secret** information that you need to connect to your database and *Open Humans*. This file should not be available online! An example file can be found in `.env.sample`.

#### The `config.yaml`

This file contain a number of details. First of all are the metadata that will decide on the style of the main page, how your project will be called throughout the application etc.

```
# REQUIRED: What's the name of your project?
project_title: My Open Humans Project
# REQUIRED: Will be displayed on the front page of the uploader
project_description: This template demonstrates how you can run your own Open Humans data upload project.
# REQUIRED: Where can we find your project on Open Humans
oh_activity_page: https://www.openhumans.org/activity/your-project-url/
```

The `app_base_url` tells the *Open Humans Uploader* where it will be located. It's
important to get this right. Amongst other things this will also decide on what the `REDIRECT URL` is.
For your local development you can keep `http://127.0.0.1:5000`. If you deploy to *heroku* you might
want to change this.

```
# REQUIRED: which URL will lead to your Open Humans uploader
app_base_url: http://127.0.0.1:5000
```

Files that are uploaded to *Open Humans* require metadata that describe the files
along with some tags. These two parameters set the metadata for your uploads:

```
# REQUIRED: Tell Open Humans what kind of data is being uploaded
file_description: This is an example file that doesnt have any meaning.
# REQUIRED: Tags to add to your file uploads
file_tags:
- tags
- 'are a good way to'
- 'describe the files you are uploading'
```

Optionally you can also specify your own logo for your project. It will be displayed
prominently on the front page.

```
# Give the path to the logo of your project.
logo: ' static/example_logo.png'

# Is there a larger project website where more info might be located?
more_info_link: http://www.github.com/gedankenstuecke/oh_data_uploader
```

#### The `.env` file
In addition to the public parameters you will need to set the parameters that 

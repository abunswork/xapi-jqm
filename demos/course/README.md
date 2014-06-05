xapi-jqm based course demo
--------------------------

This is a fully functional course that teaches a learner about the process of making french toast and quizes their knowledge. It uses [jQuery Mobile](http://www.jquerymobile.com) for layout and interactions, combined with [xAPIWrapper](https://github.com/adlnet/xAPIWrapper) to send, and retrieve data from a Learning Record Store (LRS).

The [functions.js](js/functions.js) file does all the heavy lifting by pulling values from the HTML to build statements and send them on specific events (such as page change).

You can find isolated examples for specific functionality in the demos/templates directory.

### Setup

This course was designed to run both on a web server or a local file system. If you're unfamiliar with using git to clone the repository, you can [download a zip file](https://github.com/adlnet/xapi-jqm/zipball/master) with the latest changes.

#### Configuration

The default credentials are setup to work with and account on the ADL LRS in the [config.js](js/config.js) file. You can edit this file to point to your own LRS and/or user.

**Example LRS credentials**

```
Config.endpoint = "https://lrs.adlnet.gov/xapi/";
Config.user = "jqm";
Config.password = "xapijqm";
```

You can [register your own LRS user](http://lrs.adlnet.gov) on the ADL LRS.

##### "Global Variables"

The [config.js](js/config.js) file also includes "global" variables, that are used in the building of statements. You can define variables you wish to use throughout your course with these.

**Example:**

```js
var courseID = "http://adlnet.gov/xapi/samples/xapi-jqm";
var quizID = "http://adlnet.gov/xapi/samples/xapi-jqm/quiz/"

var courseType = "http://adlnet.gov/xapi/activities/course";
var linkType = "http://adlnet.gov/xapi/activities/link";
var quizType = "http://adlnet.gov/xapi/activities/quiz";
```

### Statements Built from Attributes in HTML

A [statement](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#statement) is built in JSON that gets sent to your LRS of choice.

#### The HTML Attributes Used to Build the Statements


The ```data-chapter``` attribute defines what chapter you're in:

```html
<body data-chapter="steps">
```

Pages in jQuery Mobile (jQM) are defined as divs with a ```data-role="page"```:

```html
<div data-role="page" id="p2">
  <h2>My Content</h2>
</div>
```

#### An Overview of a Statement

The statement below includes some helper functions from the [functions.js](js/functions.js) file. These functions will be covered in [another document not yet written]().

```js
var stmt = {
    "actor": actor,
    "verb": ADL.verbs.experienced,
    "context": {
        "contextActivities": {
            "parent": [
                {
                    "id": courseID,
                    "definition": {
                        "name": {
                            "en-US": "xAPI for jQuery Demo"
                        },
                        "description": {
                            "en-US": "A sample HTML5 mobile app with xAPI tracking."
                        }
                    },
                    "objectType": "Activity"
                }
            ]
        }
    },
    "object": {
        "id" : activityID,
        "objectType": "Activity",
        "definition": {
            "name": {
                "en-US": "xAPI jQuery Mobile " + chapter + " " + pagename
            },
            "type": linkType
        }
    }
};
```

### The State API

The [State API](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#stateapi) stores state information on the LRS, such as the current chapter and page.

### Templates

This course is built with multiple examples of commonly used widgets. Below offers a brief overview of how they are used in xapi-jqm. For more detailed information please refer to [this document that doesn't exist yet]().

#### Table of Contents

Provide a list of steps that can be tracked for their completed progress through a "chapter"

#### Glossary

Layout a list of words and track which words a user has read

#### Checklist

*in progress (not yet reporting)*

#### Video Tracking

Utilizes popcorn.js and xapipopcorn.js to track videos

*in progress*

#### Quiz

Quizes can be built from three types of inputs:

- Checklist (mulitple choice)
- Radio (single choice)
- Text Box (strict string comparison)

*in progress*

#### Modal (pop-up) Windows

A template for a trigger that opens a modal a.k.a. pop-up window.

### Reporting

[Click here to view visual reports](http://adlnet.github.io/xapi-jqm/reports)

To view raw statements, log into to the [ADL LRS](https://lrs.adlnet.gov):

**username:** *jqm*

**password:** *xapijqm*
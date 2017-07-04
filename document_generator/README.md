## Angular application - connect to Document Generator

In order to use Document generator template with angular applications you need to upload zip file in d!nk admin.
Once you have your publication you can select your publication and click on **Document generator** icon.
Next you will need to add form fields.
You have 2 options:
* manually enter data
* upload JSON

If you have JSON ready you can click on "UPLOAD JSON" button. You can than input valid JSON (you can check your JSON with "check and show JSON" button).
Example of valid JSON:

    {
        "OpenQuestion": {
            "label": "OpenQuestion",
            "values": [],
            "name": "OpenQuestion",
            "type": "text"
        },
        "slider": {
            "values": [
                "0",
                "1",
                "2",
                "3",
                "4",
                "5",
                "6",
                "7",
                "8",
                "9",
                "10"
            ],
            "type": "slider",
            "name": "slider",
            "label": "slider"
        },
        "multipleChoice": {
            "label": "multiple choice",
            "values": [
                "mcoption1",
                "mcoption2",
                "mcoption3",
                "mcoption4"
            ],
            "name": "multipleChoice",
            "type": "checkbox"
        },
        "hotzone": {
            "values": [
                "hotzoneoption1",
                "hotzoneoption2",
                "hotzoneoption3",
                "hotzoneoption4",
                "hotzoneoption5"
            ],
            "name": "hotzone",
            "type": "graphicSelect",
            "label": "hotzone"
        },
        "survey_CalculateResult": {
            "text_values": [],
            "label": "CalculateResult",
            "values": [],
            "name": "CalculateResult",
            "type": "calculatedResult"
        }
    }

where "type" is one of:

    VALID_FORM_TYPES = [
        'select',
        'list',
        'table',
        'radio',
        'input',
        'number',
        'calculatedResult',
        'text',
        'checkbox',
        'slider',
        'graphicSelect',
        'textarea',
        'date',
        'image'
    ]

If type is one of:

    'input', 'number', 'calculatedResult', 'text', 'date', 'textarea', 'image'

"values" can not be empty.   

**It is important to notice that Key for each dict in JSON is same as Key that will be sent in event payload after submit is cliked in the app.**
*name* must be same as key of dict item.


Events for **latest active edition only** are considered in creating PDF.

For registering an event you can use this code:

    var payload = { test : "some_value"};
    var payloadJson = JSON.stringify(payload);
    var eventString = 'NAME_OF_EVENT';
    var storyId = 1;
    DKPlugin.recordAnalyticEvent(storyId,eventString,payloadJson,successCallbackFn,failureCallbackFn);

The storyId has to be an integer. But since Angular apps are not using stories I suggest you use 1 for the first view, 2 for the second view in your app etc.

You can retrieve information about the current customer by calling *DKPlugin.getCurrentSession*.

Here's an example:

    var obj = {
     successCallback : function(result){
       var s = angular.fromJson(result);  
       if(s.hasOwnProperty('customer')){
         console.log(s.customer.name);
       }
     },
     failureCallback : function(result){ console.log("not ok"); },
     callbackIdentifier : 'your_callback_identifier'
    };
    DKPlugin.getCurrentSession(obj);

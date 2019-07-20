## Creating a new widget

There are some widgets that are created for you to get started with:

There are two modes a widget should be able to display:

1. Preview mode:
	- In this mode you have to display a small component which will be displayed along with the card in the files view.
	- This component can be clicked to get the full preview.

This is how your component will look like in the preview mode:

![Preview Mode](assets/img/preview-mode.png)

1. Full Mode:
	- This mode should ideally be loaded into a modal using the ``` React.createPortal()``` and passing in modal-root as the element id.
	
This is how your component will look like in the Full mode:

![Full Mode](assets/img/Full-mode.png)

This should ideally create a full screen widget, but you can choose to overlay over the content if you wish to do so. Rclone can control the opening and closing of the modal.


You may copy this template to create your own Widget.

```js
import React, {useState} from "react";
import {Button, Modal} from "reactstrap";
import * as ReactDOM from "react-dom";
import {MODAL_ROOT_ELEMENT} from "../../utils/Constants";
import * as PropTypes from "prop-types";
import ErrorBoundary from "../../ErrorHandling/ErrorBoundary";

function MyWidget({playbackURL, MimeType}) {

    const [preview, setPreview] = useState(true);

    function hideFull(e) {
        e.stopPropagation();
        setPreview(!preview);

    }

    let element;
    if (preview) {
        element = (
            //  Render element in preview mode. 
        )
    } else {

        // Load the video


        element = ReactDOM.createPortal((
            //  Render element in full modal mode.
        ), document.getElementById(MODAL_ROOT_ELEMENT));
    }

    return (
        <ErrorBoundary>
            {element}
        </ErrorBoundary>
    )


}

VideoPlayer.propTypes = {
    // Define PropTypes supplied here.
    playbackURL: PropTypes.string.isRequired,
    MimeType: PropTypes.string.isRequired
};

export default VideoPlayer;

```
In MediaWidget.js add the component:

Eg:
You can replace the parameters as required.
The following parameters are available to be passed:
1. fsInfo - Gives information about the underlying remote config and capabilities.
1. Downloadable URL: downloadURL
1. Item details of the current file (as provided by rclone).
1. IP_Address
1. MimeType
1. InViewPort: Boolean. Denotes if the item is currently visible in the viewport.
1. 

Edit and add the following line to the ```MediaWidget.js```
Handle your own MimeType eg ```video/mp4```, ```image/jpeg```
```js
case "video/mp4":
    return (<VideoPlayer playbackURL={downloadURL} MimeType={MimeType} currentPath={currentPath}/>);
```
    
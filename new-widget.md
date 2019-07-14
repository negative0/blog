## Creating a new widget

There are some widgets that are created for you to get started with:

There are two modes a widget should be able to display:

1. Preview mode:
	- In this mode you have to display a small component which will be displayed along with the card in the files view.
	- This component can be clicked to get the full preview.


1. Full Mode:
	- This mode should ideally be loaded into a modal using the ```js React.createPortal()``` and passing in modal-root as the element id.
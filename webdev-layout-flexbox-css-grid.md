# flexbox

The Flexible Box Module, usually referred to as flexbox, was designed as a one-dimensional layout model either as a row or as a column.

main axis, cross axis

    align-content
    align-items
    align-self
    flex
    flex-basis
    flex-direction
    flex-flow
    flex-grow
    flex-shrink
    flex-wrap
    justify-content
    order


## flexbox container

    .flexbox-container {
        display:flex;
        flex-direction:<row|row-reverse|column|column-reverse>;
        flex-wrap:<nowrap|wrap|wrap-reverse|initial|inherit>;

	flex-flow: flex-direction flex-wrap
        
        justify-content: <flex-start|flex-end|center|space-between|space-around|initial|inherit>;
	align-items: <flex-start|flex-end|center|baseline|stretch>; 
	align-content: <flex-start|flex-end|center|baseline|stretch>; 
    }


## flexbox items

        .flexbox-items {
            flex: <flex-grow> <flex-shrink> <flex-basis>;

            align-items: <strech|flex-start|center|flex-end|flex-end|baseline>
            align-content: <stretch|center|flex-start|flex-end|space-between|space-around|initial|inherit;>;
            align-self: <stretch|flex-start|center|flex-end|baseline>
	
	    order:<integer>
        }

        <flex-grow> a positive number that determines how much extra spacde this flex item should get relative to its siblings
        <flex-shrink> a positive number is just a number and it only has meaning when compared to its sibling flex-shrink values
        <flex-basics> if flex-direction on flexbox-container is row or row-reverse it governs the width of item
                      if flex-direction on flexbox-container is column or colum-reverse it governs the height of item

## multiline flex container

While flexbox is a one dimensional model, it is possible to cause our flex items to wrap onto multiple lines. In doing so, you should consider each line as a new flex container. 



## nesting flexbox
















# css-grid layout

The css grid layout, was designed as a two-dimensional layout model which controls columns and rows together.


    grid-template-columns
    grid-template-rows
    grid-template-areas
    grid-template
    grid-auto-columns
    grid-auto-rows
    grid-auto-flow
    grid
    grid-row-start
    grid-column-start
    grid-row-end
    grid-column-end
    grid-row
    grid-column
    grid-area
    grid-row-gap
    grid-column-gap
    grid-gap

css functions

    repeat()
    minmax()
    fit-content()




    .wrapper{
        display:<grid|inline-grid>;

        grid-template-columns:<length> <percentage> <flex> <max-content> <min-content> <minmax(min, max)>
        grid-template-rows:<length> <percentage> <flex> <max-content> <min-content> <minmax(min, max)>
	        
        grid-template-columns:<px px px|fr fr fr>
        grid-template-columns: 20px repeat(6, 1fr) 20px;
        
        grid-auto-rows: minmax(100px, auto)
        grid-gap:
    }

        .grid-item{
            grid-column: <grid-column-start> / <grid-column-end>
            grid-row: <integer> / <integer>

	    grid-area: <grid-row-start>/<grid-column-start>/<grid-row-end>/<grid-column-end>

            grid-column-start: integer <span integer>
            grid-column-end:
            grid-row-start:
            grid-row-end:

	    order: <integer>
        }




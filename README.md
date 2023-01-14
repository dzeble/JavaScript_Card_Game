# JavaScript_Card_Game
Hunt the Ace, find the ace hidden among 3 other randomly shuffled cards.

## Styling
I used html and css for the visual aspects with some imported code features for the 'play game' button and the text font style

Cards were arranged using grid positioning to evenly space them out

### Positioning of the cards

html code for the classes

```html
        <div class="card-container">
            <div class="card-pos-a">

            </div>
            <div class="card-pos-b">
                
            </div>
            <div class="card-pos-c">

            </div>
            <div class="card-pos-d">
                
            </div>
        </div>
```
corresponding css code for the grid layout

```css
.card-container{
    position: relative;
    height: 100%;
    width:calc(var(--card-width-lg) * (var(--num-cards)/2) + var(--card-horizontal-space-lg));
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    grid-template-areas: "a b"
                         "c d";
    
}

.card-pos-a{
    grid-area: a;

}
.card-pos-b{
    grid-area: b;

}
.card-pos-c{
    grid-area: c;

}
.card-pos-d{
    grid-area: d;

}

.card-pos-a, .card-pos-b,.card-pos-c,.card-pos-d{
    display:flex;
    justify-content: center;
    align-items: center;
}


```


### Styling for the sides of the card and the flip effect

```css
.card-inner{
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.6s;
    transform-style: preserve-3d;
}
.card-front, .card-back{
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}
.card-img{
    height: 100%;

}
.card-back{
    transform: rotateY(180deg);
}

.card-inner.flip-it{
    transform: rotateY(180deg);
}
```

## Functionalities

I used JavaScript for the functionalities like keeping scores, card animation, rounds and the overall game play


### Creating the cards dynamically 

An array of objects, each representing a card

```js

const cardObjectDefinitions = [
    {id:1, imagePath: '/JavaScript_Card_Game/images/card-KingHearts.png'},
    {id:2, imagePath: '/JavaScript_Card_Game/images/card-JackClubs.png'},
    {id:3, imagePath: '/JavaScript_Card_Game/images/card-QueenDiamonds.png'},
    {id:4, imagePath: '/JavaScript_Card_Game/images/card-AceSpades.png'}
]
```

Function to create a card

```js
function createCard(cardItem){
    //create div elements that make up a card
    const cardElem = createElement('div')
    const cardInnerElem = createElement('div')
    const cardFrontElem = createElement('div')
    const cardBackElem = createElement('div')

    //create front and back images for a card
    const cardFrontImg = createElement('img')
    const cardBackImg = createElement('img')

    // adding class and id to the card element
    addClassToElement(cardElem,'card')
    addClassToElement(cardElem,'fly-in')
    addIdToElement(cardElem, cardItem.id)

    //add class to inner card element
    addClassToElement(cardInnerElem,'card-inner')

    //add class to front card element
    addClassToElement(cardFrontElem,'card-front')

    //add class to back card element
    addClassToElement(cardBackElem,'card-back')

    //add src attribute and appropriate value to image element - back of card
    addSrcToImageElement(cardBackImg, cardBackImgPath)

    //add src attribute and appropriate value to image element - front of card
    addSrcToImageElement(cardFrontImg, cardItem.imagePath)

    //assign class to back image element of the back of the card
    addClassToElement(cardBackImg, 'card-img')

    //assign class to front image element of the front of the card
    addClassToElement(cardFrontImg, 'card-img')


    // add front image element as child element to front card element
    addChildElement(cardFrontElem, cardFrontImg)

    // add back image element as child element to back card element
    addChildElement(cardBackElem, cardBackImg)

    // add front image element as child element to inner card element
    addChildElement(cardInnerElem, cardFrontElem)

    // add back image element as child element to inner card element
    addChildElement(cardInnerElem, cardBackElem)

    // add inner card element as child element to card element
    addChildElement(cardElem, cardInnerElem)

    //add card element as child element to appropriate grid cell
    addCardToGridCell(cardElem)

    initializeCardPositions(cardElem)

    attatchClickEventHandlerToCard(cardElem)

}
```

functions needed to create a card

```js
//re-usable function to create an html element
function createElement(elemType){
    return document.createElement(elemType)
}
//re-usable function that adds a class to an html element
function addClassToElement(elem, className){
    elem.classList.add(className)
}
//assing an id to each card
function addIdToElement(elem, id){
    elem.id = id
}
function addSrcToImageElement(imgElem, src){
    imgElem.src = src
}
function addChildElement(parentElem, childElem){
    parentElem.appendChild(childElem)
}
```

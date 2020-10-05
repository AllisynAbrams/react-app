# Project Overview

- What is a panda prize?
- ![What is a panda prize?](https://www.discoveraudit.org/wp-content/uploads/2018/01/technical-skills-larger-file.gif)

## Project Links

- [github repo](https://github.com/AllisynAbrams/react-app)
- live project: tbd

## Project Description

For this project, I plan to make a pet listings app. I will use React's Link and Source to provide access to the list of all pets, each pet's individual details, and the user's favorited pets. The pet images and details will be populated using fetch to make an API call. 

On page load/mount, a request will be made to the PetFinder API and the image and details of each pet in the PetListings component will show on the screen, along with an "add to favorites" button (each pet and associated info will show in a "card").
When a user clicks on a pet card, it will route to the SinglePetDetails component and render more details for that pet, along with a mailto button to email about that specific pet. On this page there will also be a button linking to the petlistings for the user to easily click to go back to all pet listings.


## API

hhttps://api.petfinder.com/v2/animals

TEST to get data from API - successfully rrendered the URL to each individual animal page in App.js

export default function App() {
  
  const [animals, setAnimals] = useState([])

// Used this article as basis to make the API call.  
// https://dojo.domo.com/t5/Domo-Developer/Tutorial-build-your-own-connector-against-petfinder-API/td-p/48593#

// It requires an initial call to get a Bearer Token which is then used in a second call to retrieve the data
const getToken = async () => {
  const client_id = 'ibOcZPb7jS41hAMJi3oLQWM9oj6h0alpVMmAwBktJZiLeRhYj6'
  const client_secret = 'lTZW5iz2bA84aDs4fz09e9yArV5qbJNMpIYGycv3'


  // FIRST FETCH CALL
  const res = await fetch("https://api.petfinder.com/v2/oauth2/token", {
    body: `grant_type=client_credentials&client_id=${client_id}&client_secret=${client_secret}`,
    headers: {
      "Content-Type": "application/x-www-form-urlencoded"
    },
    method: "POST"
  })
  const json = await res.json()
  const token = json.access_token
  

  // SECOND FETCH CALL
  const petRes = await  fetch("https://api.petfinder.com/v2/animals", 
    {
    headers: {
      Authorization: `Bearer ${token}`
    }
    })
  const petJson = await petRes.json()
  // THE DATA YOU SEE IN THE CONSOLE
  // console.log('this is petJson from App', petJson)
  // console.log('this is petJson.animals[0]', petJson.animals[0].type)
  console.log('this is petJson.animals', petJson.animals)
  setAnimals(petJson.animals)


}

// useEffect w empty depend array makes it so whatever is inside of it 
// only happens once on mount/load (in this case the function to call the API)
useEffect (() => {
  getToken();
 },[]);

//  ternary conditional to say, if the animals aray (at least first item) is defined/TRUE (AKA available from 
// the api call now), then map over the animals array and return the url of each item/index,
// otherwise display 'loading..'

const displayAnimals = 
(animals[0]) ? animals.map((animal, index) => {
  console.log('this is animals.url', animals[index].url)
  return <p>{animal.url}</p>
})  : 'LOADING....'

console.log('this is displayAnimals', displayAnimals)
console.log('this is animals in useState', animals)


return (
  <>
    {displayAnimals}
  </>
  )
};



## Wireframes

Upload images of wireframe to cloudinary and add the link here with a description of the specific wireframe. Also, define the the React components and the architectural design of your app.

wireframes:
- [mobile pet listings (home/main)](https://res.cloudinary.com/dv7inaqe9/image/upload/v1601906278/mobile_-_pet_listings_home_vlkhxs.jpg)
- [mobile sinlge pet details page](https://res.cloudinary.com/dv7inaqe9/image/upload/v1601908077/mobile_singlepetdetails_cwb0ar.jpg)

architecture:
- TBD


### MVP/PostMVP - 5min

The functionality will then be divided into two separate lists: MPV and PostMVP.  Carefully decided what is placed into your MVP as the client will expect this functionality to be implemented upon project completion.  

#### MVP EXAMPLE
- Functional pet listings app
	- All pet images/info wil be populated by an API call and each will be formated in some type of card format
	- Under each pet card there will be a button the user can click to add the above pet to his/her favorites
	- User can click a pet card and be directed to a page with further details about that pet, as well as a contact method to reach out about that pet
	
- Navbar with options that link to their corresponding pages (home (aka all pet listings), favorites, contact us)

- Favorites page that displays the pet cards of the pets "favorited" by the user 
	- under each pet card there will be a button that allows the user to remove that pet from their favorites


#### PostMVP EXAMPLE

- Filter bar on the pet listings page that allows the user to see only dogs, only cats, or only pets of other species
- in the pet listings page, have an up arrow that always stays at the bottom of the view and can be clicked by the user to go back to the top of the page

## Components
##### Writing out your components and its descriptions isn't a required part of the proposal but can be helpful.

Based on the initial logic defined in the previous sections try and breakdown the logic further into stateless/stateful components. 

| Component | Description | 
| --- | :---: |  
| App | Sets up app with React Router | 
| Header | Renders the header, including the nav | 
| Footer | Renders the footer |
| Main | Contains Switch/Routes for content |
| Gameboard | Renders the trivia game, contains score as state |
| Question | Renders current question via API call and Answer components |
| Answer | Renders a possible answer using props from Question |
| Score | Renders player's score received through props |
| HighScore | Form that renders at end of game if the player achieves a high score |
| Options | Renders a form of selectable game options |
| Instructions | Renders rules and info about the game |
| Leaderboard | Renders list of top scorers via API call |

Time frames are also key in the development cycle.  You have limited time to code all phases of the game.  Your estimates can then be used to evalute game possibilities based on time needed and the actual time you have before game must be submitted. It's always best to pad the time by a few hours so that you account for the unknown so add and additional hour or two to each component to play it safe. Also, put a gif at the top of your Readme before you pitch, and you'll get a panda prize.

Unless otherwise noted, time is listed in hours:

|  Component  |  Priority  |  Estimated Time  |  Actual Time  |
|  ---  |  :---:  |   :---:  |  :---:  |
| Create React app and files for all components | high | 1 | 1 |
| header/navbar (reactstrap or bootstrap - need to look into this?) | high | 2 | 2 |
| banner | low | 0.5 | 0.5 |
| set up React routing | high | 2 | 2 |
| make API call and practice displaying data | high | 1.5 | 1.5 |
| display and format/style pet listings | high | 3 | 3 |
| make add to favorites button add to favorites component on click | high | 3 | 3 |
| make add to favorites button add to favorites component on click | high | 3 | 3 |
| make remove from favorites button remove from favorites  component on click | high | 2 | 2 |
| display/format single pet listing page | high | 3 | 3 |
| contact section - adding and styling contact form | med | 1 | 1 |
| media queries for tablet responsive  | high | 1 | 1 |
| media queries for desktop responsive  | high | 1 | 1 |
| figure out how to deploy on netlify | high | 2 | 2 |
| testing & de-bugging | high | 2 | 2 |
| choose fonts and color scheme | med | 2 | 2 |
|  Total  | H | 30 | 30 |

## Additional Libraries
ReactStrap - responsive navbar
????? would this be bootstrap ????


## Code Snippet

Use this section to include a brief code snippet of functionality that you are proud of and a brief description.  Code snippet should not be greater than 10 lines of code.

The below code is how the leaderboard is populated. The shorter the name, the more dots are added between the name and score. The font size is set progressively smaller for each entry.

```
let fontSize = props.gameView ? 24 : 42

scoreList = props.highScores.map((highScore, i) => {
	let dots = ' . . . '   
	for (let j = highScore.name.length; j < 12; j += 2) {
		dots += '. '
	}
	if (i > 0) {
		let mult = (i < 3 ? 2 : 1)
		props.gameView ? fontSize -= 1 * mult : fontSize -= 3 * mult
	}
```
...
```
	return (
		<li style={{fontSize: `${fontSize}px`, color: color}} key={i}>
			<span className="bold">{`${i + 1}) `}</span>
			{highScore.name} {dots} {highScore.score}
		</li>
	) 
})
```

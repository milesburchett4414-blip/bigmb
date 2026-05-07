@@ -0,0 +1,65 @@


// the search bar  //

const userData = [
  {  body: 'Slime knight', imageUrl: 'assets/images/Slime_night.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/slime-knight")'},
  {  body: 'Pixels for christmas', imageUrl: 'assets/images/pixels_for_chris.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/pixels-for-christmas")' },
  {  body: 'Plangman', imageUrl: 'assets/images/plangman.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/plangman")' },
  {  body: 'Space rescue', imageUrl: 'assets/images/space_rescue.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/space-rescue")' },
  {  body: 'Doom Shooter', imageUrl: 'assets/images/doom.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/doomsday-shooter")' }  ,
  {  body: 'Rock paper clicker', imageUrl: 'assets/images/rock_paper.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/rock-paper-clicker")' }  ,
  {  body: 'Magirune 2', imageUrl: 'assets/images/magirune 2.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/magirune-2")' }  ,
  {  body: 'One chance', imageUrl: 'assets/images/one chance.png', linkUrl: 'javascript:startGame("https://www.crazygames.fr/embed/one-chance")' }
]
const userCardTemplate = document.querySelector("[data-user-template]")
const userCardContainer = document.querySelector("[data-user-cards-container]")
const searchInput = document.querySelector("[data-search]");

let users = []

searchInput.addEventListener("input", e => {
  const value = e.target.value.toLowerCase()
  console.log(value)
  users.forEach(user => {
    const isVisible = user.name.toLowerCase().includes(value)
   user.element.classList.toggle("hide",!isVisible)    
  }); 
   
})

users = userData.map((user) => {
  const card1 = userCardTemplate.content.cloneNode(true).children[0];
  const header1 = card1.querySelector("[data-header1]");
  const body1 = card1.querySelector("[data-body]");
  const logoImg1 = document.createElement('img');
  const link1 = document.createElement('a');

  logoImg1.src = user.imageUrl;
  logoImg1.width = 300; 
  logoImg1.height = 300;
  link1.appendChild(logoImg1);
  link1.href = user.linkUrl;
  header1.appendChild(link1);
  body1.textContent = user.body;

  userCardContainer.append(card1);
  return {name: user.body , element : card1}
});


// the search bar //

function startGame(gameSrc) {
  document.getElementById("gameFrame").src = gameSrc;
  document.querySelector("#gameSection").scrollIntoView();
}

window.onload = function() {
  const urlParams = new URLSearchParams(window.location.search);
    const gameUrl = urlParams.get('gameUrl');
    if (gameUrl) {
      document.getElementById('gameFrame').src = gameUrl;
      document.querySelector("#gameSection").scrollIntoView();
    }
}

<template>
  <div class="settings-background" id="settings-backblur"></div>

  <div class="settings fadeInDown" id="settings-popup">
    <div>
      <h1>
        Settings
      </h1>
      <div class="choser" id="choser">
        <button class="generalbtn" id="generalbtn">General</button>
        <button id="appearancebtn">Appearance</button>
      </div>
      <div class="general-settings" id="general-settings">
        <div>
          <p>Discord Rich Presence</p>
          <label class="switch">
            <input type="checkbox" id="setting-enableRPC">
            <div>
              <span></span>
            </div>
          </label>
        </div>

        <div>
          <p>Launch on Startup</p>
          <label class="switch">
            <input type="checkbox" id="setting-launchOnStartup" disabled="readonly">
            <div>
              <span></span>
            </div>
          </label>
        </div>

        <div>
          <p>Skip Login Menu</p>
          <label class="switch">
            <input type="checkbox" id="setting-skipLogin" disabled="readonly">
            <div>
              <span></span>
            </div>
          </label>
        </div>

        <div>
          <p>Minimize to Tray on Launch</p>
          <label class="switch">
            <input type="checkbox" id="setting-trayMinLaunch">
            <div>
              <span></span>
            </div>
          </label>
        </div>

        <div>
          <p>Minimize to Tray on Quit</p>
          <label class="switch">
            <input type="checkbox" id="setting-trayMinQuit">
            <div>
              <span></span>
            </div>
          </label>
        </div>

        <div>
          <p>Check for Updates</p>
          <label class="switch">
            <input type="checkbox" id="setting-checkForUpdates" disabled="readonly">
            <div>
              <span></span>
            </div>
          </label>
        </div>
      </div>
      <div class="appearance-settings" id="appearance-settings">
        <div id="a">
          <p>Accent Color</p>
          <div class="btnInput">
            <label class="color">
              <input type="color" id="setting-accentColor">
            </label>
            <img class="repeatButton"
              src="./assets/icons/reset.png">
          </div>
        </div>
      </div>

      <div class="settings-footer">
        v0.6.1 (Tauri Release)
      </div>
    </div>
  </div>

  <div class="main-loading-overlay" id="main-loading-overlay">
    <div class="spinner-content">
      <img src="./assets/svg/spinner.svg" class="loading-spinner">
      <p id="spinnerLoading">Loading...</p>
    </div>
  </div>

  <div data-tauri-drag-region class="titlebar">
    <div data-tauri-drag-region style="justify-content: space-between;" class="titlebar-icons">
      <div class="titlebar-options">
        <img class="titlebar-settings" src="./assets/svg/settings.svg" id="settings-btn">
        <img class="titlebar-account" src="./assets/svg/account.svg" id="account-btn">
        <img class="titlebar-update" src="./assets/svg/download.svg" id="update-btn">
        <img class="titlebar-loading" src="./assets/svg/loading-spinner.svg" id="loadingbtn">
      </div>
      <div style="margin-top: 0px;" class="titlebar-icons">
        <div @click="min_window" class="titlebar-min mx-1"></div>
        <div @click="max_window" class="titlebar-max mx-1"></div>
        <div @click="close_window" class="titlebar-exit mx-1"></div>
      </div>
    </div>
  </div>

  <div class="bg" id="bg">
    <div class="outline"></div>
    <div class="homebox" id="home">
      <div class="children fadeInUp">
        <img class="head-pic" src="./assets/img/main-banner.png" id="head-pic">
      </div>
      <div class="children fadeInDown">
        <div class="jump-back">
          <p>Recently Launched</p>
          <div id="recentGamesListMainPage" class="fadeInDown mainPageGamesList"></div>
        </div>
      </div>
      <div class="children fadeInLeft">
        <div class="online-friends">
          <p>Online Friends</p>
          <div class="CMS">Coming Soon...</div>
        </div>
      </div>
    </div>

    <div class="secondorybox" id="recent">
      <p>Recently Played</p>
      <div id="recentGamesList" class="fadeInDown gamesList">
      </div>
    </div>

    <div class="secondorybox" id="games">
      <div class="addGamePopUp" id="addGamePopUp">
        <div class="mainSection fadeInDown">
          <div class="section">
            <div class="title">Game Name</div>
            <input maxlength="24" type="text" class="inputGameName" id="inputGameName">
          </div>
          <div class="section">
            <button class="addGameLocation" id="addGameLocation">Locate Game</button>
          </div>
          <div class="section">
            <button class="addGameFinalBtn" id="addGameFinalBtn">Add Game</button>
          </div>
        </div>
        <div class="addGameBannerSection fadeInUp">
          <label for="addGameCustomBanner"></label>
          <input class="banner" id="addGameCustomBanner" type="file" accept="image/png"
            @change="(event) => loadCustomBanner(event)" />
          <p id="addGameCustomBannerTxt">Hover & Click to Select Banner</p>
          <div id="addGameCustomBannerOutput" class="addGameCustomBannerOutput"></div>

        </div>
      </div>

      <div id="game-loading-overlay" class="game-loading-overlay">
        <div class="spinner-content">
          <img src="./assets/svg/spinner.svg" alt="Loading..." class="loading-spinner">
        </div>
      </div>
      <p>All Games</p>
      <svg id="addGameBtn" class="addGameBtn" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px" y="0px" width="459.325px" height="459.325px" viewBox="0 0 459.325 459.325"
        style="enable-background:new 0 0 459.325 459.325;" xml:space="preserve">
        <g>
          <path fill="var(--svgcolor)" d="M459.319,229.668c0,22.201-17.992,40.193-40.205,40.193H269.85v149.271c0,22.207-17.998,40.199-40.196,40.193
		c-11.101,0-21.149-4.492-28.416-11.763c-7.276-7.281-11.774-17.324-11.769-28.419l-0.006-149.288H40.181
		c-11.094,0-21.134-4.492-28.416-11.774c-7.264-7.264-11.759-17.312-11.759-28.413C0,207.471,17.992,189.475,40.202,189.475h149.267
		V40.202C189.469,17.998,207.471,0,229.671,0c22.192,0.006,40.178,17.986,40.19,40.187v149.288h149.282
		C441.339,189.487,459.308,207.471,459.319,229.668z" />
        </g>

      </svg>

      <div class="search-bar">
        <input type="text" placeholder="Search" id="gamesInput">
      </div>
      <div id="allGamesList" class="fadeInDown gamesList">
      </div>
    </div>

    <div class="secondorybox" id="favs">
      <p>Favourite Games</p>
      <div class="search-bar">
        <input type="text" placeholder="Search" id="favsInput">
      </div>
      <div id="favGamesList" class="fadeInDown gamesList">
      </div>
    </div>

    <div class="secondorybox" id="messages">
      <p>Messages</p>
    </div>

    <div class="secondorybox" id="activity">
      <p>Activity</p>
    </div>

    <div class="secondorybox" id="friends">
      <p>Friends</p>
    </div>

    <div class="gameMenu" id="gameMenu">
        <div class="gameMenuTitle" id="gameMenuTitle"></div>
        <div class="gameMenuBtns">
          <button class="gameMenuBtn" id="removeGame">Remove Game</button>
        </div>
    </div>

    <div class="leftbar">
      <div class="d-flex justify-content-center">
        <div>
          <div class="user-pfp">
            <label for="file"></label>
            <input id="file" type="file" accept="image/png" @change="(event) => loadPFP(event)" />
            <img src="./assets/svg/default-profile.svg" alt="Avatar" width="88" id="output">
          </div>
          <input class="username" id="text" type="text" value="Lazap" spellcheck="false" maxlength="12" />
        </div>
      </div>

      <div class="side-tabs">
        <div class="d-flex justify-content-center pb-2">
          <div class="side-tab" id="home-btn">
            <div class="indicator" id="indicator"></div>
            <img src="./assets/svg/home.svg" height="25" width="25">
            <div class="side-tab-text">
              Home
            </div>
          </div>
        </div>

        <div class="category-name d-flex justify-content-left">
          Games
        </div>
        <div class="d-flex justify-content-center">
          <div class="side-tab" id="recent-btn">
            <img id="recently-btn-img" src="./assets/svg/recent.svg" height="25" width="25">
            <div class="side-tab-text">
              Recent
            </div>
          </div>
        </div>
        <div class="d-flex justify-content-center">
          <div class="side-tab" id="games-btn">
            <img id="games-btn-img" src="./assets/svg/games.svg" height="25" width="25">
            <div class="side-tab-text">
              All Games
            </div>
          </div>
        </div>
        <div class="d-flex justify-content-center pb-2">
          <div class="side-tab" id="favs-btn">
            <img id="favs-btn-img" src="./assets/svg/favs.svg" height="25" width="25">
            <div class="side-tab-text">
              Favourites
            </div>
          </div>
        </div>



        <div class="category-name d-flex justify-content-start">
          Friends
        </div>
        <div class="d-flex justify-content-center">
          <div class="side-tab" id="messages-btn">
            <img src="./assets/svg/messages.svg" height="25" width="25">
            <div class="side-tab-text">
              Messages
            </div>
          </div>
        </div>
        <div class="d-flex justify-content-center">
          <div class="side-tab" id="activity-btn">
            <img src="./assets/svg/activity.svg" height="25" width="25">
            <div class="side-tab-text">
              Activity
            </div>
          </div>
        </div>
        <div class="d-flex justify-content-center">
          <div class="side-tab" id="friends-btn">
            <img src="./assets/svg/friends.svg" height="25" width="25">
            <div class="side-tab-text">
              All Friends
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import listeners from './components/listeners.vue'
import storage from './components/storage.vue'

export default {
  async created() {
    const os = window.__TAURI__.os;
    console.info(`OS: ${await os.platform()} | Arch: ${await os.arch()}`);

    if (await os.platform() === "win32") {
      document.getElementById('bg').style.height = '111.5vh';
    }
  },
  listeners,
  storage,
  methods: {
    min_window() {
      window.__TAURI__.window.appWindow.minimize()
    },
    max_window() {
      window.__TAURI__.window.appWindow.toggleMaximize()
    },
    close_window() {
      window.__TAURI__.window.appWindow.close()
    },
    async loadPFP(event) {
      var selectedFile = event.target.files[0];
      var reader = new FileReader();

      reader.onload = async function () {
        await window.__TAURI__.fs.writeBinaryFile(await window.__TAURI__.path.appDir() + `storage/cache/user/pfp.png`, reader.result);
        document.getElementById("output").src = window.__TAURI__.tauri.convertFileSrc(await window.__TAURI__.path.appDir() + `storage/cache/user/pfp.png`) + `?${new Date().getSeconds()}`;
      };
      reader.readAsArrayBuffer(selectedFile);
    },
    async loadCustomBanner(event) {
      var selectedFile = event.target.files[0];
      var reader = new FileReader();

      reader.onload = async function () {
        await window.__TAURI__.fs.writeBinaryFile(await window.__TAURI__.path.appDir() + `storage/cache/games/banners/newcustombanner.png`, reader.result);
        document.getElementById("addGameCustomBannerOutput").style.backgroundImage = `url(` + window.__TAURI__.tauri.convertFileSrc(await window.__TAURI__.path.appDir() + `storage/cache/games/banners/newcustombanner.png`) + `?${new Date().getSeconds()}` + `)`;
      };
      document.getElementById("addGameCustomBannerTxt").style.opacity = "0"
      reader.readAsArrayBuffer(selectedFile);
    }
  }
};
</script>


 <style>
 @import './css/default.css';
 </style>

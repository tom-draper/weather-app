<template>
  <div id="app" :class="temperatureClass()">
    <div
      id="app-highlight"
      :class="temperatureHighlightClass()"
      v-on:keydown="handleArrow"
    >
      <main>
        <div class="top-bar">
          <div class="search-box">
            <input
              type="text"
              class="search-bar"
              placeholder="Search..."
              v-model="query"
              @keyup.enter="fetchWeather"
            />
          </div>
          <div class="location-box" v-if="typeof weather.main != 'undefined'">
            <div class="location">
              {{ weather.name }}, {{ weather.sys.country }}
            </div>
          </div>
        </div>
        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="weather-box">
            <div class="temp">
              {{ Math.round(weather.main.temp) }}<span class="degrees">°C</span>
            </div>
            <div class="weather">{{ weather.weather[0].main }}</div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: process.env.VUE_APP_API_KEY,
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather() {
      fetch(
        `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    temperatureClass() {
      if (typeof this.weather.main != "undefined") {
        return (
          "temp" +
          Math.max(Math.min(Math.round(this.weather.main.temp), 40), -1)
        );
      } else {
        return "";
      }
    },
    temperatureHighlightClass() {
      if (typeof this.weather.main != "undefined") {
        return (
          "highlight" +
          Math.max(Math.min(Math.round(this.weather.main.temp), 40), -1)
        );
      } else {
        return "";
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
    tempClass() {
      let tClass = "no-temp";
      console.log(this.weather);
      if (typeof this.weather.main != "undefined") {
        tClass = "temp-" + this.weather.main.temp;
      }
      console.log(tClass);
      return tClass;
    },
    inc() {
      this.weather.main.temp += 1;
    },
    dec() {
      this.weather.main.temp -= 1;
    },
    handleArrow(event) {
      console.log(event.keyCode);
      if (event.keyCode == 38) {
        this.inc();
      } else if (event.keyCode == 40) {
        this.dec();
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,900;1,900&family=Raleway:wght@600;900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Montserrat", sans-serif;
}

#app {
  background-size: cover;
  background-position: bottom;
  transition: 0.4;
  background: linear-gradient(rgb(42, 157, 211), rgb(22, 129, 230));
}

#app.temp-1 {
  background: linear-gradient(20deg, rgb(177, 241, 255), rgb(255, 255, 255));
}

#app.temp0 {
  background: linear-gradient(10deg, rgb(177, 241, 255), rgb(255, 255, 255));
}

#app.temp1 {
  background: linear-gradient(10deg, rgb(137, 233, 255), rgb(255, 255, 255));
}

#app.temp2 {
  background: linear-gradient(40deg, rgb(47, 217, 255), rgb(255, 255, 255));
}

#app.temp3 {
  background: linear-gradient(0deg, rgb(0, 208, 255), rgb(206, 228, 255));
}

#app.temp4 {
  background: linear-gradient(260deg, rgb(40, 198, 255), rgb(222, 237, 255));
}

#app.temp5 {
  background: linear-gradient(290deg, rgb(46, 189, 255), rgb(180, 214, 255));
}

#app.temp6 {
  background: linear-gradient(320deg, rgb(46, 189, 255), rgb(180, 214, 255));
}
#app.temp7 {
  background: linear-gradient(180deg, rgb(102, 207, 255), rgb(157, 227, 255));
}

#app.temp8 {
  background: linear-gradient(180deg, rgb(144, 220, 255), rgb(157, 227, 255));
}
#app.temp9 {
  background: linear-gradient(180deg, rgb(157, 227, 255), rgb(206, 244, 255));
}

#app.temp10 {
  background: linear-gradient(220deg, rgb(157, 227, 255), rgb(246, 253, 255));
}
.highlight10 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.17)
  );
}

#app.temp11 {
  background: linear-gradient(240deg, rgb(146, 224, 255), rgb(246, 253, 255));
}
.highlight11 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.17)
  );
}

#app.temp12 {
  background: linear-gradient(250deg, rgb(125, 218, 255), rgb(237, 251, 255));
}
.highlight12 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.17)
  );
}

#app.temp13 {
  background: linear-gradient(300deg, rgb(130, 211, 255), rgb(255, 251, 226));
}
.highlight13 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.17)
  );
}

#app.temp14 {
  background: linear-gradient(rgb(177, 228, 255), rgb(255, 254, 231));
}
.highlight14 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.19)
  );
}

#app.temp15 {
  background: linear-gradient(rgb(230, 250, 255), rgb(254, 255, 218));
}
.highlight15 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.213)
  );
}

#app.temp16 {
  background: linear-gradient(rgb(252, 255, 197), rgb(255, 246, 197));
}
.highlight16 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.213)
  );
}

#app.temp17 {
  background: linear-gradient(rgb(235, 237, 149), rgb(251, 230, 160));
}
.highlight17 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.213)
  );
}

#app.temp18 {
  background: linear-gradient(rgb(235, 230, 120), rgb(255, 229, 167));
}
.highlight18 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 175, 219, 0.213)
  );
}

#app.temp19 {
  background: linear-gradient(rgb(255, 220, 95), rgb(255, 220, 120));
}
.highlight19 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 143, 205, 0.213)
  );
}

#app.temp20 {
  background: linear-gradient(50deg, rgb(255, 205, 41), rgb(255, 235, 121));
}
.highlight20 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 255, 255, 0.178)
  );
}

#app.temp21 {
  background: linear-gradient(50deg, rgb(255, 205, 43), rgb(255, 231, 97));
}
.highlight21 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 255, 255, 0.178)
  );
}

#app.temp22 {
  background: linear-gradient(50deg, rgb(255, 205, 43), rgb(255, 229, 83));
}
.highlight22 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 255, 255, 0.111)
  );
}

#app.temp23 {
  background: linear-gradient(50deg, rgb(255, 205, 41), rgb(255, 226, 64));
}
.highlight23 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 255, 255, 0.07)
  );
}

#app.temp24 {
  background: linear-gradient(50deg, rgb(255, 206, 45), rgb(255, 217, 0));
}
.highlight24 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 145, 0, 0.583)
  );
}

#app.temp25 {
  background: linear-gradient(50deg, rgb(211, 144, 0), rgb(255, 196, 0));
}
.highlight25 {
  background: linear-gradient(
    100deg,
    rgba(0, 0, 0, 0),
    rgba(255, 145, 0, 0.755)
  );
}

#app.temp26 {
  background: linear-gradient(50deg, rgb(214, 104, 0), rgb(255, 183, 0));
}
.highlight26 {
  background: linear-gradient(
    40deg,
    rgba(0, 0, 0, 0),
    rgba(255, 145, 0, 0.611)
  );
}

#app.temp27 {
  background: linear-gradient(50deg, rgb(135, 31, 0), rgb(255, 111, 0));
}
.highlight27 {
  background: linear-gradient(
    40deg,
    rgba(0, 0, 0, 0),
    rgba(255, 145, 0, 0.611)
  );
}

#app.temp28 {
  background: linear-gradient(50deg, rgb(135, 0, 25), rgb(255, 81, 0));
}
.highlight28 {
  background: linear-gradient(
    40deg,
    rgba(0, 0, 0, 0),
    rgba(255, 145, 0, 0.611)
  );
}

#app.temp29 {
  background: linear-gradient(50deg, rgb(135, 36, 0), rgb(255, 0, 0));
}
.highlight29 {
  background: linear-gradient(
    40deg,
    rgba(0, 0, 0, 0),
    rgba(255, 145, 0, 0.611)
  );
}

#app.temp30 {
  background: linear-gradient(50deg, rgb(135, 0, 25), rgb(255, 0, 0));
}
.highlight30 {
  background: linear-gradient(0deg, rgba(0, 0, 0, 0), rgba(255, 145, 0, 0.522));
}

#app.temp31 {
  background: linear-gradient(50deg, rgb(135, 0, 25), rgb(221, 0, 0));
}
.highlight31 {
  background: linear-gradient(0deg, rgba(0, 0, 0, 0), rgba(255, 145, 0, 0.275));
}

#app.temp32 {
  background: linear-gradient(50deg, rgb(135, 0, 25), rgb(233, 0, 0));
}
.highlight32 {
  background: linear-gradient(0deg, rgba(0, 0, 0, 0), rgba(255, 0, 0, 0.522));
}

#app.temp33 {
  background: linear-gradient(50deg, rgb(135, 0, 25), rgb(255, 0, 0));
}
.highlight33 {
  background: linear-gradient(0deg, rgba(0, 0, 0, 0), rgba(106, 0, 133, 0.097));
}

#app.temp34 {
  background: linear-gradient(100deg, rgb(135, 0, 25), rgb(255, 0, 0));
}
.highlight34 {
  background: linear-gradient(
    90deg,
    rgba(0, 0, 0, 0),
    rgba(106, 0, 133, 0.289)
  );
}

#app.temp35 {
  background: linear-gradient(90deg, rgb(135, 0, 25), rgb(255, 0, 0));
}
.highlight35 {
  background: linear-gradient(
    40deg,
    rgba(0, 0, 0, 0),
    rgba(106, 0, 133, 0.487)
  );
}

#app.temp36 {
  background: linear-gradient(90deg, rgb(135, 0, 25), rgb(255, 0, 0));
}
.highlight36 {
  background: linear-gradient(10deg, rgba(0, 0, 0, 0), rgba(94, 0, 118, 0.522));
}

#app.temp37 {
  background: linear-gradient(90deg, rgb(135, 0, 25), rgb(255, 0, 0));
}
.highlight37 {
  background: linear-gradient(
    340deg,
    rgba(0, 0, 0, 0),
    rgba(83, 0, 104, 0.659)
  );
}

#app.temp38 {
  background: linear-gradient(10deg, rgb(121, 0, 22), rgb(255, 0, 0));
}
.highlight38 {
  background: linear-gradient(290deg, rgba(0, 0, 0, 0), rgba(60, 0, 75, 0.761));
}

#app.temp39 {
  background: linear-gradient(100deg, rgb(121, 0, 20), rgb(255, 0, 0));
}
.highlight39 {
  background: linear-gradient(240deg, rgba(0, 0, 0, 0), rgba(55, 0, 60, 0.863));
}

#app.temp40 {
  background: linear-gradient(120deg, rgb(121, 0, 20), rgb(255, 0, 0));
}
.highlight40 {
  background: linear-gradient(210deg, rgba(0, 0, 0, 0), rgb(38, 0, 41));
}

main {
  min-height: 100vh;
  padding: 25px;
}

.search-box {
  flex: 4;
}

.search-box .search-bar {
  font-family: "Raleway";
  font-weight: 600;
  display: block;
  padding: 10px 16px;

  color: #383838;
  font-size: 13px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  background-color: rgba(255, 255, 255, 0.15);
  border-radius: 16px 16px;
  transition: 0.4s;
}
::placeholder {
  /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #545454;
  opacity: 1; /* Firefox */
}

.top-bar {
  display: flex;
  margin-bottom: 30px;
}

.search-box .search-bar :focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-box {
  flex: 6;
}

.location {
  margin-top: 3px;
}

.location-box .location {
  font-family: "Raleway", sans-serif;
  font-style: italic;
  font-size: 16px;
  padding: 4px 16px;

  font-weight: 800;
  width: 100%;
  text-align: right;
}

.location-box .date {
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  color: #000;
  font-size: 200px;
  font-weight: 900;
  letter-spacing: -0.05em;

  border-radius: 16px;
  margin-top: 20vh;

  font-family: "Montserrat", sans-serif;
  font-style: italic;
}

.degrees {
  font-size: 0.5em;
  letter-spacing: -0.02em;
  margin-left: 8px;
}

.weather-box .weather {
  font-family: "Raleway", sans-serif;
  font-size: 22px;
  font-weight: 900;
  margin-top: -30px;
}

@media only screen and (max-width: 600px) {
  .weather-box .temp {
    font-size: 9.5em;
  }

  .search-box {
    flex: 3;
    max-width: 185px;
  }
  .search-bar {
    width: 100%;
  }
  .location-box {
    flex: 4;
  }
}
</style>

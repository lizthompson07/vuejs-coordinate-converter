<template>
  <div id="app">
    <div class="container" :style="{ backgroundColor: color }">
      <h1>Coordinate Converter</h1>
      <h4>Choose background colour:</h4>
      <input type="text" v-model="color">
      <hr>
      <input type="button" @click="resetValues" value="Reset starting values">
      <div class="row">
        <div class="col-2">
          <p><u>Decimal Degrees (DD)</u></p>
          <p>
            Latitude
            <input type="hidden" v-model="combinedDDBoth" id="ddboth">
            <button @click="copyToClipboard('ddboth')">Copy DD</button>
          </p>
          <input type="number" v-model="ddLat" id="ddlat" @keyup.enter="convertDDToOtherLat">&#176;
          <br>
          {{ ddLat }}
          <button @click="copyToClipboard('ddlat')">Copy</button>
          <p>Longitude</p>
          <input type="number" v-model="ddLong" id="ddlong" @keyup.enter="convertDDToOtherLong">&#176;
          <br>
          {{ ddLong }}
          <button @click="copyToClipboard('ddlong')">Copy</button>
        </div>
        <div class="col-4">
          <p><u>Degrees Decimal Minutes (DDM)</u></p>
          <p>
            Latitude
            <input type="hidden" v-model="combinedDDMBoth" id="ddmboth">
            <button @click="copyToClipboard('ddmboth')">Copy DDM</button>
          </p>
          <input type="number" v-model="ddmLatDegree" @keyup.enter="convertDDMToOtherLat">&#176;
          <input type="number" v-model="ddmLatMinute" @keyup.enter="convertDDMToOtherLat">&#8242;
          <br>
          <input type="hidden" v-model="combinedDDMLat" id="ddmlat">
          {{ combinedDDMLat }}
          <button @click="copyToClipboard('ddmlat')">Copy</button>
          <p>Longitude</p>
          <input type="number" v-model="ddmLongDegree" @keyup.enter="convertDDMToOtherLong">&#176;
          <input type="number" v-model="ddmLongMinute" @keyup.enter="convertDDMToOtherLong">&#8242;
          <br>
          <input type="hidden" v-model="combinedDDMLong" id="ddmlong">
          {{ combinedDDMLong }}
          <button @click="copyToClipboard('ddmlong')">Copy</button>

        </div>
        <div class="col-sm">
          <p><u>Degrees Minutes Seconds (DMS)</u></p>
          <p>
            Latitude
            <input type="hidden" v-model="combinedDMSBoth" id="dmsboth">
            <button @click="copyToClipboard('dmsboth')">Copy DMS</button>
          </p>
          <input type="number" v-model="dmsLatDegree" @keyup.enter="convertDMSToOtherLat">&#176;
          <input type="number" v-model="dmsLatMinute" @keyup.enter="convertDMSToOtherLat">&#8242;
          <input type="number" v-model="dmsLatSecond" @keyup.enter="convertDMSToOtherLat">&#8243;
          <br>
          <input type="hidden" v-model="combinedDMSLat" id="dmslat">
          {{ combinedDMSLat }}
          <button @click="copyToClipboard('dmslat')">Copy</button>
          <p>Longitude</p>
          <input type="number" v-model="dmsLongDegree" @keyup.enter="convertDMSToOtherLong">&#176;
          <input type="number" v-model="dmsLongMinute" @keyup.enter="convertDMSToOtherLong">&#8242;
          <input type="number" v-model="dmsLongSecond" @keyup.enter="convertDMSToOtherLong">&#8243;
          <br>
          <input type="hidden" v-model="combinedDMSLong" id="dmslong">
          {{ combinedDMSLong }}
          <button @click="copyToClipboard('dmslong')">Copy</button>
        </div>
      </div>
    </div>
<!--    <br>-->
<!--    <hr>-->
<!--    <input type="number" v-model="test1">-->
<!--    <input type="number" v-model="test2">-->
<!--    <br>-->

<!--    {{ testMethod1 }}-->
<!--    {{ testMethod2 }}-->
  </div>
</template>

<script>
export default {
  name: 'ConverterComponent',
      data() {
        return {
            color: "beige",
            num: 5,
            ddLat: 45.508333,
            ddLong: -63.754167,
            ddmLatDegree: 45,
            ddmLatMinute: 30.5,
            ddmLongDegree: 63,
            ddmLongMinute: 45.25,
            dmsLatDegree: 45,
            dmsLatMinute: 30,
            dmsLatSecond: 29.9988,
            dmsLongDegree: 63,
            dmsLongMinute: 45,
            dmsLongSecond: 15.0012,
            supportsCB: false,
            message: '',
            test1: 123,
            test2: 321,
        }
    },
    computed: {
        // testMethod1() {
        //     let reverse = this.test1.toString().split("").reverse().join("");
        //     this.test2 = parseInt(reverse);
        //     // return parseInt(reverse);
        // },
        // testMethod2() {
        //     let reverse = this.test2.toString().split("").reverse().join("");
        //     this.test1 = parseInt(reverse);
        //     // return parseInt(reverse);
        // },
        combinedDDBoth() {
            return "" + this.ddLat + ", " + this.ddLong;
        },
        combinedDDMLat() {
            return "" + this.ddmLatDegree + " " + this.ddmLatMinute;
        },
        combinedDDMLong() {
            return "" + this.ddmLongDegree + " " + this.ddmLongMinute;
        },
        combinedDDMBoth() {
            return "" + this.ddmLatDegree + " " + this.ddmLatMinute + " " + "N" + " " + this.ddmLongDegree + " " + this.ddmLongMinute + " " + "W";
        },
        combinedDMSLat() {
            return "" + this.dmsLatDegree + " " + this.dmsLatMinute + " " + this.dmsLatSecond;
        },
        combinedDMSLong() {
            return "" + this.dmsLongDegree + " " + this.dmsLongMinute + " " + this.dmsLongSecond;
        },
        combinedDMSBoth() {
            return "" + this.dmsLatDegree + " " + this.dmsLatMinute + " " + this.dmsLatSecond + " " + "N" + " " + this.dmsLongDegree + " " + this.dmsLongMinute + " " + this.dmsLongSecond + " " + "W";
        },
        // convertDDMToDDLat() {
        //     var degree = this.ddmLatDegree;
        //     var minute = this.ddmLatMinute / 60;
        //     this.ddLat = (degree + minute).toFixed(6);
        //     // return (degree + minute).toFixed(6);
        //     // return "" + (this.ddmLatDegree + (this.ddmLatMinute / 60))
        // },
        // convertDDMToDDLong() {
        //     var degree = this.ddmLongDegree;
        //     var minute = this.ddmLongMinute / 60;
        //     this.ddLong = -(degree + minute).toFixed(6);
        //     // return (degree + minute).toFixed(6);
        //     // return "" + (this.ddmLongDegree + (this.ddmLongMinute / 60))
        // },
        // convertDDToDDMLat() {
        //     // let minute = this.ddLat.toString().split(".")[1];
        //     // let newminutes = minute[1] / 100 * 60;
        //     let degree = Math.trunc(this.ddLat);
        //     let minute = Number((this.ddLat-degree).toFixed(6));
        //     this.ddmLatDegree = degree;
        //     this.ddmLatMinute = minute * 60;
        //     // return minute
        // }
    },
    methods: {
        copyToClipboard(id) {
            var copyText = document.getElementById(id).value;
            navigator.clipboard.writeText(copyText)
                .then(() => {
                    console.log('Text is on the clipboard.');
                    this.message = 'Code copied to clipboard';
                })
                .catch(e => {
                    console.error(e);
                    this.message = 'Sorry, unable to copy to clipboard'
                });
        },
        resetValues() {
            Object.assign(this.$data, this.$options.data.call(this));
        },
        convertDDMToOtherLat() {
            //convert DDM to DD
            var degree = this.ddmLatDegree;
            var minute = this.ddmLatMinute / 60;
            //set ddLat to the new values
            this.ddLat = (degree + minute).toFixed(6);
            //convert DDM to DMS
            let minutes = Math.trunc(this.ddmLatMinute);
            let second = Number((this.ddmLatMinute - minutes).toFixed(6));
            //set dmsLatDegree, dmsLatMinute, dmsLatSecond to new values
            //add error catching if minutes >= 60
            if (minutes > 60.0) {
                alert("Minutes should not be over 60, check again.");
            } else if (minutes === 60) {
                let minutes = 0;
                this.dmsLatDegree = degree + 1;
                this.dmsLatMinute = minutes;
                this.dmsLatSecond = second * 60;
            } else {
                this.dmsLatDegree = this.ddmLatDegree
                this.dmsLatMinute = minutes;
                this.dmsLatSecond = second * 60;
            }
        },
        convertDDMToOtherLong() {
            //convert DDM to DD
            var degree = this.ddmLongDegree;
            var minute = this.ddmLongMinute / 60;
            //set ddLong to the new values
            this.ddLong = -(degree + minute).toFixed(6);
            //convert DDM to DMS
            let minutes = Math.trunc(this.ddmLongMinute);
            let second = Number((this.ddmLongMinute - minutes).toFixed(6));
            //set dmsLongDegree, dmsLongMinute, dmsLongSecond to new values
            //add error catching if minutes > 60
            if (minutes > 60.0) {
                alert("Minutes should not be over 60, check again.");
            } else if (minutes === 60) {
                let minutes = 0;
                this.dmsLongDegree = degree + 1;
                this.dmsLongMinute = minutes;
                this.dmsLongSecond = second * 60;
            } else {
                this.dmsLongDegree = this.ddmLongDegree;
                this.dmsLongMinute = minutes;
                this.dmsLongSecond = second * 60;
            }
        },
        convertDDToOtherLat() {
            //convert DD to DDM
            let degree = Math.trunc(this.ddLat);
            let minute = Number((this.ddLat - degree).toFixed(6));
            //set ddmLatDegree, ddmLatMinute to the new values
            this.ddmLatDegree = degree;
            this.ddmLatMinute = minute * 60;
            //convert DDM to DMS
            let minutes = Math.trunc(this.ddmLatMinute);
            let second = Number((this.ddmLatMinute - minutes).toFixed(6));
            //set dmsLatDegree, dmsLatMinute, dmsLatSecond to new values
            this.dmsLatDegree = this.ddmLatDegree;
            this.dmsLatMinute = minutes;
            this.dmsLatSecond = second * 60;
        },
        convertDDToOtherLong() {
            //convert DD to DDM
            let degree = Math.trunc(this.ddLong);
            let minute = Number((this.ddLong - degree).toFixed(6));
            //set ddmLatDegree, ddmLatMinute to the new values
            this.ddmLongDegree = degree;
            this.ddmLongMinute = minute * 60;
            //convert DDM to DMS
            let minutes = Math.trunc(this.ddmLongMinute);
            let second = Number((this.ddmLongMinute - minutes).toFixed(6));
            //set dmsLongDegree, dmsLongMinute, dmsLongSecond to new values
            this.dmsLongDegree = this.ddmLongDegree
            this.dmsLongMinute = minutes;
            this.dmsLongSecond = second * 60;
        },
        convertDMSToOtherLat() {
            //convert DMS to DDM
            let minute = this.dmsLatMinute;
            let second = this.dmsLatSecond / 60;
            //set ddmLatDegree, ddmLatMinute to the new values
            //add error catching if seconds > 60
            if ((this.dmsLatSecond > 60.0) || (this.dmsLatMinute > 60.0)) {
                alert("Minutes and Seconds should not be over 60, check again.");
            } else if (this.dmsLatSecond === 60) {
                this.ddmLatDegree = this.dmsLatDegree;
                this.ddmLatMinute = minute + 1;
            } else if ((this.dmsLatMinute + second) > 59.999999) {
                this.ddmLatDegree = this.dmsLatDegree + 1;
                this.ddmLatMinute = second.toFixed(6);
            } else {
                this.ddmLatDegree = this.dmsLatDegree;
                this.ddmLatMinute = (minute + second).toFixed(6);
            }
            //convert DDM to DD
            var degree = this.ddmLatDegree;
            var minutes = this.ddmLatMinute / 60;
            //set ddLat to the new values
            this.ddLat = (degree + minutes).toFixed(6);
        },
        convertDMSToOtherLong() {
            //convert DMS to DDM
            let minute = this.dmsLongMinute;
            let second = this.dmsLongSecond / 60;
            //set ddmLongDegree, ddmLongMinute to the new values
            //add error catching if seconds > 60
            if ((this.dmsLongSecond > 60.0) || (this.dmsLongMinute > 60.0)) {
                alert("Minutes and Seconds should not be over 60, check again.");
            } else if (this.dmsLongSecond === 60) {
                this.ddmLongDegree = this.dmsLongDegree;
                this.ddmLongMinute = minute + 1;
            } else if ((this.dmsLongMinute + second) > 59.999999) {
                this.ddmLongDegree = this.dmsLongDegree + 1;
                this.ddmLongMinute = second.toFixed(6);
            } else {
                this.ddmLongDegree = this.dmsLongDegree;
                this.ddmLongMinute = (minute + second).toFixed(6);
            }
            //convert DDM to DD
            var degree = this.ddmLongDegree;
            var minutes = this.ddmLongMinute / 60;
            //set ddLat to the new values
            this.ddLong = (degree + minutes).toFixed(6);
        }
    },
    created() {
        if (navigator.clipboard) {
            this.supportsCB = true;
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin: 30px;
}

p {
  font-weight: bold;
}
</style>

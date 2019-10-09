<template>
  <div id="form">
    <div id="slogan">CLIMB THE TAB EVEREST</div>
    <img src="../assets/logos.png" alt />
    <div id="form-container">
      <div class="header">WARNING, ACKNOWLEDGEMENT, CONSENT AND WAIVER FORM - NSW</div>
      <div
        class="normal-text"
      >Between: Tab Limited (TAB), its subsidiaries and related entities and the undersigned person.</div>
      <div class="header">Warning and Acknowlegement</div>
      <div class="normal-text">
        I acknowledge that my participation in The TAB Spring Carnival Live Site 'Climb the TAB Everest' promotion
        (Promotion):
        <br />contains inherent risks in all aspects of physical activity and may involve risk of personal injury
        (including death) and/or possible property damage;
        <br />may involve strenuous bodyweight exercises and other high exertion activities and that it is my right to
        refuse such participation at any time during my allocation time; and I acknowledge that I understand the
        possible strenuous nature of the activity and the potential for undesirable physiological results
        including, but not limited to, abnormal blood pressure, muscle soreness, fainting, heart attack and/or
        death.
        <br />
        <br />I warrant that I do not suffer from any medical condition that may affect my ability to participate
        safely in strenuous exercise and hereby acknowledge that my participation in the Promotion is voluntary
        and I knowingly assume all the risks.
      </div>
      <div class="header">Release</div>
      <div class="normal-text">
        I give consent to TAB, its employees, agents and its related entities taking and using (or permitting
        authorised third parties to use) images (photographs or video) and/or sounds recordings of me that it
        has obtained or produced and reference to my first name (the Content) in any public media (including
        social media), radio, television, internet or print, or in a TAB publication, without any restriction on
        use (time, geographic, number of times of use, or otherwise).
        <br />
        <br />I understand and acknowledge that such Content may contain my personal information and that the intended
        use of such Content is for TAB's advertising, marketing or promotional purposes, and without expectation
        of compensation or other benefit to me.
        <br />
        <br />I hereby waive the right to or interest in the Content disclosed to the public, as contemplated in this
        release, and to the extent that any benefit accrues to TAB from the use of the Content, I hereby and
        forever waive any interest in or claim to such benefits.
        <br />
        <br />I hereby release and forever discharge TAB (including without limitaion all of its officers, employees,
        contractors and agents) from any and all claims, liability, actions, suits, demands, costs, expenses or
        indebtedness arising out of, related to, or in any way connected with the use of the Content, and I
        hereby waive all rights and interest in and to such materials.
      </div>
      <div class="header">General</div>
      <div class="normal-text">
        I confirm that I am over 18 years of age and that I have full legal capacity to be bound by this
        contract, and that I am signing this contract of my own free will and accord.
        <br />
        <br />This form is governed by the laws of New South Wales. To the extend that a Court finds that any
        provision of this form or part thereof is invalid or unenforceable, that provision or part thereof will
        be severed and the remainder of this form will remain valid and enforceable.
        <br />
        <br />I declare that I have read understood and agree with the above warning, acknowledgement, consent and
        waiver and acknowledge that I fully understand the meaning and importance of its contents and I assume
        with full knowledge of any and all dangers in my participation in the Prize and do so at my own risk.
      </div>
      <label class="checkbox-label">
        I am over the age of 18
        <input type="checkbox" v-model="eligible" />
      </label>
      <label class="checkbox-label">
        I accept the terms and conditions of the Promotion
        <input type="checkbox" v-model="terms" />
      </label>
      <br />
      <br />
      <label>
        <span class="form-label">First Name</span>
        <input type="text" v-model="first_name" placeholder="First Name" />
      </label>
      <br />
      <label>
        <span class="form-label">Last Name</span>
        <input type="text" v-model="last_name" placeholder="Last Name" />
      </label>
      <br />
      <label>
        <span class="form-label">Player Name</span>
        <input type="text" v-model="player_name" placeholder="Player Name" maxlength="10"/>
      </label>
      <br />
      <label>
        <span class="form-label">Date of Birth</span>
      </label>
      <input type="number" v-model="day" placeholder="01" />
      <input type="number" v-model="month" placeholder="10" />
      <input type="number" v-model="year" placeholder="1980" />

      <br />
      <label>
        <span class="form-label">Mobile</span>
        <input type="text" v-model="mobile" placeholder="Mobile number" />
      </label>
      <br />
      <label>
        <span class="form-label">Email</span>
        <input type="text" v-model="email" placeholder="Email" />
      </label>
      <br />
      <br />
      <label class="checkbox-label">
        Are you a TAB customer?
        <span style="position: absolute; right: -10vmin">
          <label class="radio-label">
            Yes
            <input type="radio" value="true" v-model="customer" />
          </label>
          <label class="radio-label">
            No
            <input type="radio" value="false" v-model="customer" />
          </label>
        </span>
      </label>
      <label class="checkbox-label">
        I consent to receive marketing communications information on upcoming events from the Australian Turf Club
        <input
          type="checkbox"
          v-model="marketing"
        />
      </label>
      <br />
      <br />
      <br />
      <label class="checkbox-label">
        I consent to receive marketing communications information on upcoming events from TAB
        <input
          type="checkbox"
          v-model="terms"
        />
      </label>
      <br />
      <br />
      <div class="header">PRIVACY STATEMENT</div>
      <div class="normal-text">
        The purpose of TAB collecting your personal details on this form is to verify that you are the person providing the acknowledgement, consent and waiver and identified in the Content. Your personal details may be disclosed to TAB's related bodies corporate, representatives and agents, and also to third party social media providers. Those third party social media providers may have servers located in overseas jurisdictions. Unless you tell TAB otherwise, TAB will assume you consent to the above collection, use and disclosure.
        <br />For more information see TAB's Privacy Policy at www.tabcorp.com.au/privacy.
        <br />For privacy related queries, please contact +61 3 9868 2890 or email privacy@tabcorp.com.au.
      </div>
      <span id="signature">Signature</span>
      <canvas id="canvas" width="500px" height="250px"></canvas>

      <button class="left" @click="toSelect">BACK</button>
      <button class="right" @click="submitPlayer">FINISH</button>
    </div>
  </div>
</template>

<script>
/*

*/
import axios from "axios";
const qs = require("querystring");
import SignaturePad from "signature_pad";

export default {
  name: "Form",
  data: function() {
    return {
      eligible: false,
      terms: false,
      first_name: "",
      last_name: "",
      player_name: "",
      day: null,
      month: null,
      year: null,
      mobile: "",
      email: "",
      customer: false,
      marketing: false,
      signaturePad: null
    };
  },
  methods: {
    clearCanvas: function() {},
    toSelect: function() {
      this.$emit("to-select");
    },
    submitPlayer: function() {
      const config = {
        headers: {
          "Content-Type": "application/x-www-form-urlencoded"
        }
      };

      const url = "http://192.168.0.77:3000/form";
      const requestBody = {
        eligible: this.eligible,
        terms: this.terms,
        first_name: this.first_name,
        last_name: this.last_name,
        player_name: this.player_name,
        date_of_birth: this.day + "/" + this.month + "/" + this.year,
        mobile: this.mobile,
        email: this.email,
        customer: this.customer,
        marketing: this.marketing
      };

      axios
        .post(url, qs.stringify(requestBody), config)
        .then(result => {
          this.$emit("select-player", result.data.player);
          const canvas = document.getElementById("canvas");
          axios.post(
            "http://192.168.0.77:3000/signature",
            qs.stringify({ img: canvas.toDataURL(), id: result.data.player.id })
          );
        })
        .catch(err => {
          console.log(err);
        });

      /*
      //document.getElementById('inp_img').value = canvas.toDataURL();
      let formData = new FormData();
      formData.append("img", canvas.toDataURL());
      let request = new XMLHttpRequest();
      request.open("POST", "http://127.0.0.1:3000/signature");
      request.send(formData);
      */
    }
  },
  mounted() {
    const canvas = document.getElementById("canvas");
    this.signaturePad = new SignaturePad(canvas);
  }
};
</script>

<style scoped>
#signature {
  font-size: 4vmin;
  margin-bottom: 0;
}
#canvas {
  display: block;
  margin: auto;
  margin-top: 2vmin;
  background: white;
  border-radius: 10px;
}
img {
  height: 7vmin;
  float: right;
  margin-top: 1vmin;
  margin-bottom: 3vmin;
}
.radio-label {
  margin-left: 2vmin;
  font-size: 3vmin;
}
input[type="radio"] {
  -webkit-appearance: checkbox;
  position: relative;
  width: 4vmin;
  height: 4vmin;
  float: right;
}
input[type="checkbox"] {
  position: absolute;
  width: 4vmin;
  height: 4vmin;
  right: -10vmin;
}
.checkbox-label {
  width: 100vmin;
  height: 8vmin;
  font-size: 3vmin;
  text-align: left;
  max-width: 70vmin;
}

.form-label {
  display: inline-block;
  width: 28vmin;
  text-align: left;
}
label {
  position: relative;
  float: left;
  font-size: 4vmin;
  font-family: gilroy_regular;
}
input[type="number"] {
  position: relative;
  display: inline-block;
  width: 12vmin;
  height: 5vmin;
  border: none;
  border-radius: 0.5vmin;
  font-family: gilroy_regular;
  font-size: 3vmin;

  margin-right: 4vmin;
  margin-bottom: 1.4vmin;
  text-align: center;
}
input[type="text"] {
  display: inline-block;
  width: 43vmin;
  height: 5vmin;
  border: none;
  border-radius: 0.5vmin;
  padding-left: 1vmin;
  font-family: gilroy_regular;
  font-size: 3vmin;
}
#form {
  width: 90vw;
  height: 100vh;
  margin: auto;
  overflow: hidden;
}
#slogan {
  margin-top: 2vmin;
  color: white;
  font-family: gilroy_bold;
  font-size: 5.75vmin;
  text-align: right;
}

.header {
  text-align: left;
  color: white;
  font-family: "gilroy_bold";
  font-size: 4vmin;
  margin-bottom: 4vw;
}
.normal-text {
  text-align: left;
  color: rgba(255, 255, 255, 0.9);
  font-family: "gilroy_light";
  font-size: 3vmin;
  margin-bottom: 4vw;
  line-height: 3.3vw;
}
#form-container {
  display: block;
  margin: 5vmin auto;
  width: 90%;
  padding: 0 4vmin;
  height: 80%;
  font-size: 6.5vmin;
  font-family: gilroy_regular;

  border: 0.5vmin solid #35ea78;
  border-radius: 1vmin;
  background: #018543;
  text-decoration: none;

  color: white;
  overflow: scroll;
}

button {
  position: relative;
  display: inline-block;
  width: 33%;
  height: 10%;
  font-size: 6.5vmin;
  font-family: gilroy_regular;

  border: 0.5vmin solid #35ea78;
  border-radius: 1vmin;
  background: #018543;
  text-decoration: none;

  color: white;
  margin-top: 4vmin;
  margin-bottom: 3vmin;
}

.left {
  float: left;
}

.right {
  float: right;
}
</style>
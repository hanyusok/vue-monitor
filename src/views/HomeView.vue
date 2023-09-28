<script>
import fb from "node-firebird";
import { reactive, computed } from "vue";

const options = {
  // host :  '192.168.0.13',
  host: "127.0.0.1",
  port: 3050,
  //database: databaseStr,
  database:
    "/Library/Frameworks/firebird.framework/Versions/A/Resources/examples/empbuild/employee.fdb",
  //database :  'C:\\Program Files\\Firebird\\Firebird_2_5\\examples\\empbuild\\EMPLOYEE.FDB',
  // database :  'C:\\Mts3\\Db\\MTSDB.FDB',
  user: "SYSDBA",
  password: "masterkey",
  lowercase_keys: false,
  role: null,
  pageSize: 4096,
};

// let fbResult = reactive([]);
let sql = "";
sql = "SELECT * FROM EMPLOYEE";

export default {
  data() {
    return {
      fbResult: [],
    };
  },

  // const getfbData = computed(() => {
  // const getfbData = () => {
  // let fbResult = reactive([]);
  mounted() {
    fb.attach(options, (err, db) => {
      if (err) {
        console.error("Error connecting to the database: ", err);
        return;
      }
      db.query(slq, (err, result) => {
        if (err) {
          console.error("Error executing the query: ", err);
          return;
        }
        fbResult = result;

        db.detach();
      });
    });
  },
};
</script>

<template>
  <h1>home</h1>
  <h4>Result:</h4>
  <!-- <button @click="getfbData">get data</button> -->
  <div v-bind="fbResult"></div>
</template>

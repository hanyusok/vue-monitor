<script setup>
import fb from "node-firebird";
import {
  reactive,
  computed,
  ref,
  onMounted,
  onUpdated,
  onBeforeMount,
} from "vue";
import { Buffer } from "buffer";

const fbResult = ref([]);
const sql = ref("");
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

onMounted(() => {
  console.log("mounting...");

  fb.attach(options, (err, db) => {
    if (err) {
      console.error("Error connecting to the database: ", err);
      return;
    }

    sql.value = "SELECT * FROM EMPLOYEE";

    db.query(slq, (err, result) => {
      if (err) {
        console.error("Error executing the query: ", err);
        return;
      }
      fbResult.value = result;

      db.detach();
    });
  });
});
</script>

<template>
  <h1>home</h1>
  <h4>Options:</h4>
  <p>{{ options.value }}</p>
  <!-- <button @click="getfbData">get data</button> -->
  <!-- <div v-bind="fbResult"></div> -->
  <p>Results:</p>
  <p>{{ fbResult.value }}</p>
</template>

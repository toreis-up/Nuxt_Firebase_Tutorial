<template>
  <div>
    <input v-model="formData" />
    <button @click="send">送信</button>
  </div>
</template>

<script>
import { getFirestore, collection, addDoc } from "firebase/firestore";

export default {
  data() {
    return {
      formData: "",
    };
  },
  methods: {
    async send() {
      const db = await getFirestore(); // Firestoreのルートを持ってくる
      const hogeColRef = await collection(db, "hogehoge"); // hogehogeコレクションができる
      const fugaDocRef = await addDoc(hogeColRef, { name: "fugafuga" }); // nameというフィールド(値はfugafuga)を持つドキュメントができる
      const contColRef = await collection(fugaDocRef, "content"); // contentコレクションができる
      const msgRef = await addDoc(contColRef, { msg: this.formData }); // msgというフィールド(値はformData)を持つドキュメントができる

      console.log(msgRef);
      this.formData = ""; // キレイにする
    },
  },
};
</script>

<style>
</style>

<template>
  <div id="app">
    <b-form @submit="onSubmit">
      <div>
        <b-card no-body>
          <b-tabs card>
            <b-tab title="Tab 1" active @click="tabClick()">
              <b-card-text>
                <div class="img-wrap">
                  <div v-if="!image">첫번째 이미지 등록해주세요</div>
                  <img v-else :src="image" />
                </div>
                <div>
                  <!-- TODO b-form-file에서 v-model 을 쓰면 에러가 난다. 왜 ?? -->
                  <b-form-file
                    id="file-default"
                    placeholder="이미지를 등록해주세요"
                    @change="onFileChange"
                  ></b-form-file>
                  <b-button @click="removeImage">Remove image</b-button>
                </div>
              </b-card-text>
            </b-tab>
          </b-tabs>
        </b-card>
      </div>
      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      image: "",
      file1: null,
    };
  },
  methods: {
    onFileChange(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length) return;
      this.createImage(files[0]);
    },
    createImage(file) {
      // let image = new Image();
      let reader = new FileReader();
      let vm = this;

      reader.onload = (e) => {
        vm.image = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    removeImage() {
      this.image = "";
    },
    onSubmit(e) {
      e.preventDefault();
      console.log(this.image);
    },
    tabClick() {
      console.log("tab click!");
    },
  },
};
</script>

<style>
.img-wrap {
  vertical-align: center;
  height: 300px;
}
#app {
  text-align: center;
}
img {
  height: 300px;
  margin: auto;
  display: block;
  margin-bottom: 10px;
}
</style>

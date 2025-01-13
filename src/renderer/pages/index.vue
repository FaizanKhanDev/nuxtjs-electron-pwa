<template>
  <v-container fluid style="padding: 0">
    <v-card style="padding: 20px">
      <v-form ref="form">
        <v-row>
          <!-- First Row -->
          <v-col cols="12" md="4">
            <v-text-field
              :rules="[rules.required]"
              v-model="formData.recordId"
              label="Record ID"
              outlined
              dense
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              :rules="[rules.required]"
              v-model="formData.date"
              label="Date"
              outlined
              dense
            ></v-text-field>
          </v-col>

          <v-col cols="12" md="4">
            <v-text-field
              :rules="[rules.required]"
              v-model="formData.customerName"
              label="Customer Name"
              outlined
              dense
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              :rules="[rules.required]"
              v-model="formData.address"
              label="Address"
              outlined
              dense
            ></v-text-field>
          </v-col>

          <!-- Second Row -->
          <v-col cols="12" md="4">
            <v-text-field
              :rules="[rules.required]"
              v-model="formData.city"
              label="City"
              outlined
              dense
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="formData.country"
              :rules="[rules.required]"
              label="Country"
              outlined
              dense
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="formData.phoneNo"
              label="Phone No"
              outlined
              dense
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="formData.phoneNo"
              :rules="[rules.required]"
              label="Cell Phone"
              outlined
              dense
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="formData.email"
              :rules="[rules.required]"
              label="Email"
              outlined
              dense
              type="email"
            ></v-text-field>
          </v-col>
        </v-row>

        <!-- Thumbnail Upload Section -->
        <v-row>
          <v-col cols="12" md="6">
            <p
              class="text-subtitle-1"
              style="font-weight: bold; margin-bottom: 10px"
            >
              Thumbnail Upload:
            </p>
            <v-sheet
              class="drop-zone pa-6"
              height="150"
              outlined
              @dragover.prevent
              @drop.prevent="handleDrop"
              @click="triggerFileInput"
            >
              <div class="text-center">
                Drop Zone to upload PNG or JPEG files
              </div>
              <input
                type="file"
                ref="fileInput"
                style="display: none"
                accept=".png,.jpg,.jpeg"
                multiple
                @change="handleFileSelect"
              />
            </v-sheet>
          </v-col>

          <!-- Thumbnails List -->
          <v-col cols="12" md="6">
            <p
              class="text-subtitle-1 mb-2"
              style="font-weight: bold; margin-bottom: 10px"
            >
              Thumbnails List:
            </p>
            <v-col
              class="thumbnails-container-list"
            >
              <v-sheet class="mx-auto" max-width="700">
                <v-slide-group multiple show-arrows>
                  <v-slide-item
                    v-for="(image, index) in thumbnails"
                    :key="index"
                  >
                    <v-img
                      :src="image"
                      height="100"
                      width="100"
                      contain
                    ></v-img>
                  </v-slide-item>
                </v-slide-group>
              </v-sheet>
            </v-col>
          </v-col>
        </v-row>

        <!-- Text Area Section -->
        <v-row>
          <v-col cols="12">
            <v-data-table
              :headers="headers"
              :items="desserts"
              :items-per-page="5"
              class="elevation-1"
            ></v-data-table>
          </v-col>
        </v-row>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "CustomerForm",
  data() {
    return {
      formData: {
        recordId: "",
        customerName: "",
        address: "",
        city: "",
        phoneNo: "",
        email: "",
        notes: "",
      },
      rules: {
        required: (value) => !!value || "This field is required.",
      },
      thumbnails: [],
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: 1,
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: 1,
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: 7,
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: 8,
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: 16,
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: 0,
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: 2,
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: 45,
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: 22,
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: 6,
        },
      ],
    };
  },
  methods: {
    handleDrop(e) {
      const files = [...e.dataTransfer.files];
      this.processFiles(files);
    },
    handleFileSelect(e) {
      const files = [...e.target.files];
      this.processFiles(files);
    },
    processFiles(files) {
      files.forEach((file) => {
        if (file.type.match("image.*")) {
          const reader = new FileReader();
          reader.onload = (e) => {
            this.thumbnails.push(e.target.result);
          };
          reader.readAsDataURL(file);
        }
      });
    },
    triggerFileInput() {
      this.$refs.fileInput.click();
    },
  },
};
</script>

<style >
* {
  font-family: "Roboto", sans-serif;
}
.theme--light.v-messages {
  color: red !important;
}

.thumbnails-container-list {
  border: 2px dashed #ccc;
  cursor: pointer;
  transition: border-color 0.3s;
}
.drop-zone {
  border: 2px dashed #ccc;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color 0.3s;
}

.drop-zone:hover {
  border-color: #1976d2;
}

.thumbnails-container {
  display: flex;
  overflow-x: auto;
  scroll-behavior: smooth;
  scrollbar-width: none;
  -ms-overflow-style: none;
  white-space: nowrap;
  padding: 0 40px;
}

.thumbnails-container::-webkit-scrollbar {
  display: none;
}

.scroll-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
}

.scroll-btn.left {
  left: 0;
}

.scroll-btn.right {
  right: 0;
}
</style>
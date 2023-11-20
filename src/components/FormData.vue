<template>
  <div class="form-container">
    <h2>methods</h2>
    <p>
      Message: <span class="bold">{{ message }}</span>
    </p>
    <form @submit.prevent="submitForm" class="data-form">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="name" />
      <label for="name">Email:</label>
      <input type="email" id="email" v-model="email" />
      <button type="submit" class="btn" :disabled="!name || !email">
        Submit
      </button>
    </form>
    <div v-if="submissions.length > 0" class="submissions">
      <h3>Submissions list:</h3>
      <ul class="list-submissions">
        <li
          v-for="(submission, index) in submissions"
          :key="index"
          class="submission">
          <p>
            Name: <span class="bold">{{ submission.name }}</span>
          </p>
          <p>
            Email: <span class="bold">{{ submission.email }}</span>
          </p>
          <button @click="deleteSubmission(index)" class="btn-delete">
            &#x2715;
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      submissions: [],
    };
  },
  methods: {
    submitForm() {
      const newSubmisiion = {
        name: this.name,
        email: this.email,
      };
      if (this.name && this.email) {
        this.submissions.push(newSubmisiion);
        this.name = "";
        this.email = "";
      }
    },
    deleteSubmission(index) {
      this.submissions.splice(index, 1);
    },
    showMessage() {
      alert("Hello !");
    },
  },
  computed: {
    message() {
      const count = this.submissions.length;
      if (count === 0) {
        return "No submissions yet!";
      } else if (count === 1) {
        return "1 Submission!";
      } else {
        return `${count} Submissions!`;
      }
    },
  },
};
</script>

<style scoped>
.data-form {
  display: flex;
  flex-direction: column;
  margin: 20px 0 0;
  gap: 10px;
}
.data-form label {
  text-align: left;
}
.data-form input {
  max-width: 100%;
  padding: 8px;
}
.btn {
  font-size: 16px;
  color: #4c82b0;
  background: #fff;
  border: 2px solid #4c82b0;
  border-radius: 3px;
  padding: 10px 20px;
  margin: 20px 0 0;
}
.btn:disabled {
  font-size: 16px;
  color: #bfc0c3;
  background: #f2f2f2;
  border: 2px solid #bfc0c3;
  border-radius: 3px;
  padding: 10px 20px;
  margin: 20px 0 0;
  cursor: pointer;
}
.submissions {
  margin: 30px 0 0;
}
.list-submissions {
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.submission {
  position: relative;
  background: #f6fbff;
  text-align: left;
  border-radius: 8px;
  padding: 10px;
}
.btn-delete {
  position: absolute;
  top: 6px;
  right: 6px;
  line-height: 1;
  background: none;
  border: 0;
  padding: 2px 6px;
  cursor: pointer;
}
.btn-delete:hover {
  color: #4c82b0;
}
</style>
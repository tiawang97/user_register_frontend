<template>
  <div id="app">
    <div class="register-container">
      <h1>あなたの情報を入力してください</h1>
      <form @submit.prevent="handleRegister">

        <h1 class="sublabel">名前</h1>
        <div class="form-group">
          <label for="firstName">姓<span style="color: #EC0000;margin-left: 1rem;">必須</span></label>
          <input 
            type="text" 
            id="firstName" 
            v-model="form.firstName" 
            required 
            @input="validateName('firstName')" 
          />
          <p v-if="errors.firstName" class="error-message">{{ errors.firstName }}</p>
          <label for="lastName">名<span style="color: #EC0000;margin-left: 1rem;">必須</span></label>
          <input 
            type="text" 
            id="lastName" 
            v-model="form.lastName" 
            required 
             @input="validateName('lastName')"
          />
          <p v-if="errors.lastName" class="error-message">{{ errors.lastName }}</p>
          <label for="firstNameAlphabet">氏（カタカナ）<span style="color: #EC0000;margin-left: 1rem;">必須</span></label>
          <input 
            type="text" 
            id="firstNameAlphabet" 
            v-model="form.firstNameAlphabet" 
            required 
            @input="validateName('firstNameAlphabet')"
          />
          <p v-if="errors.firstNameAlphabet" class="error-message">{{ errors.firstNameAlphabet }}</p>
          <label for="lastNameAlphabet">名（カタカナ）<span style="color: #EC0000;margin-left: 1rem;">必須</span></label>
          <input 
            type="text" 
            id="lastNameAlphabet" 
            v-model="form.lastNameAlphabet" 
            required 
            @input="validateName('lastNameAlphabet')"
          />
          <p v-if="errors.lastNameAlphabet" class="error-message">{{ errors.lastNameAlphabet }}</p>
        </div>

        <h1 class="sublabel">年齢・性別</h1>
        <div class="form-group">
          <label>性别<span style="color: #EC0000;margin-left: 1rem;">必須</span></label>
          <div class="gender-options">
            <label>
              <input 
                type="radio" 
                value="男性" 
                v-model="form.gender" 
              />
              男性
            </label>
            <label>
              <input 
                type="radio" 
                value="女性" 
                v-model="form.gender" 
              />
              女性
            </label>
            <label>
              <input 
                type="radio" 
                value="無回答・その他" 
                v-model="form.gender" 
              />
              無回答・その他
            </label>
          </div>
        </div>

        <label for="age">年齢<span style="color: #EC0000;margin-left: 1rem;">必須</span></label>
        <input 
          type="text" 
          id="age" 
          v-model="form.age" 
          required
          @input="validateAge"
        />
        <p v-if="errors.age" class="error-message">{{ errors.age }}</p>

        <button type="submit" class="submit-btn" :disabled="!isFormComplete || ageError">次へ</button>
        <button type="button" class="back-btn" @click="goBack">戻る</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        firstName: "", 
        lastName: "", 
        firstNameAlphabet: "", 
        lastNameAlphabet: "",
        gender: "無回答・その他",
        age: "",
      },
      errors: {
        firstName: "", 
        lastName: "",  
        firstNameAlphabet: "", 
        lastNameAlphabet: "",
        age: "",  
      },
    };
  },
  computed: {
    hasErrors() {
      return Object.values(this.errors).some(error => error !== "");
    },
    isFormComplete() {
      return (
        this.form.firstName.trim() !== "" &&
        this.form.lastName.trim() !== "" &&
        this.form.firstNameAlphabet.trim() !== "" &&
        this.form.lastNameAlphabet.trim() !== "" &&
        this.form.gender.trim() !== "" &&
        this.form.age.trim() !== ""
      );
    },
    isSubmitDisabled() {
      return this.hasErrors || !this.isFormComplete;
    },
  },
  methods: {
    validateName(field) {
      const value = this.form[field];
      const regex = /^[\u3040-\u30FF\u4E00-\u9FAFa-zA-Z]+$/; 
      if (!regex.test(value)) {
        this.errors[field] = "記号・数字は使用できません";
      } else {
        this.errors[field] = "";
      }
    },
    validateAge() {
      const age = this.form.age;
      if (!Number.isInteger(Number(age)) || age <= 0) {
        this.errors.age = "半角数字以外は使用できません";
      } else {
        this.errors.age = "";
      }
    },
    handleRegister() {
      if (this.hasErrors) {
        alert("フォームのエラーを修正してから再度送信してください！");
        return;
      }
      alert(
        `登録が成功しました！`
      );
    },
    goBack() {
      window.history.back();
    },
  },
};
</script>

<style scoped>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.register-container {
  background: #ffffff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 90%;
  max-width: 400px;
}

h1 {
  text-align: center;
  color: #333333;
  margin-bottom: 20px;
}

h1.sublabel {
    text-align: left;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
  font-weight: bold;
  color: #333333;
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #333333;
  border-radius: 4px;
  box-sizing: border-box;
}

input:focus {
  border-color: #CD820A;
  outline: none;
}

.gender-options {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.gender-options label {
  display: inline-flex;
  align-items: center;
  margin-right: 20px;
}

.gender-options input {
  width: unset;
  margin-right: 5px;
}

input#age {
    width: 20%;
}

.error-message {
  color: red;
  font-size: 14px;
}

.submit-btn {
  width: 100%;
  padding: 10px;
  background-color: #ffffff;
  color: #0017C1;
  border: 1px solid #0017C1;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

.submit-btn:hover {
  background-color: #0017C1;
  color: #ffffff;
}

.submit-btn:disabled {
  background-color: #cccccc;
  color: #ffffff;
  border: 1px solid #cccccc;
  cursor: not-allowed;
}

.back-btn {
  width: 100%;
  padding: 10px;
  background-color: #ffffff;
  color: #0017C1;
  border: 1px solid #0017C1;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

.back-btn:hover {
  background-color: #0017C1;
  color: #ffffff;
}
</style>


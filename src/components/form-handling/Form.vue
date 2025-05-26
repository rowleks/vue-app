<template>
  <main>
    <div>
      <pre class="text-left">
        {{ formdata }}
      </pre>
      <form action="" v-on:submit.prevent="handleSubmit">
        <fieldset class="personal-info">
          <legend>Personal Information</legend>

          <span>
            <label for="fullName">Full Name:</label>
            <input
              type="text"
              id="fullName"
              v-model="formdata.fullName"
              required
            />
          </span>

          <span>
            <label for="email">Email:</label>
            <input type="email" id="email" v-model="formdata.email" required />
          </span>

          <span>
            <label for="phoneNumber">Phone Number:</label>
            <input
              type="tel"
              id="phoneNumber"
              v-model="formdata.phoneNumber"
              required
            />
          </span>

          <span>
            <label>Gender:</label>
            <input
              type="radio"
              id="gender-male"
              name="gender"
              value="male"
              v-model="formdata.gender"
            />
            <label for="gender-male">Male</label>
            <input
              type="radio"
              id="gender-female"
              name="gender"
              value="female"
              v-model="formdata.gender"
            />
            <label for="gender-female">Female</label>
          </span>
        </fieldset>

        <fieldset class="prof-info">
          <legend>Professional Information</legend>
          <span>
            <label for="skills">Skills:</label>
            <div id="skills" class="flex items-center gap-4">
              <label>
                <input type="checkbox" value="vue" v-model="formdata.skills" />
                Vue.js
              </label>
              <label>
                <input
                  type="checkbox"
                  value="react"
                  v-model="formdata.skills"
                />
                React
              </label>
              <label>
                <input
                  type="checkbox"
                  value="angular"
                  v-model="formdata.skills"
                />
                Angular
              </label>
              <label>
                <input
                  type="checkbox"
                  value="javascript"
                  v-model="formdata.skills"
                />
                JavaScript
              </label>
            </div>
          </span>

          <span>
            <label for="experienceLevel">Experience Level:</label>
            <select
              id="experienceLevel"
              v-model="formdata.experienceLevel"
              required
            >
              <option value="" disabled selected>Select your level</option>
              <option value="beginner">Beginner</option>
              <option value="intermediate">Intermediate</option>
              <option value="advanced">Advanced</option>
            </select>
          </span>

          <span>
            <label for="coverLetter">Cover Letter:</label>
            <textarea
              id="coverLetter"
              v-model="formdata.coverLetter"
              rows="5"
              cols="50"
            ></textarea>
          </span>

          <span>
            <label for="resumeUpload">Resume Upload:</label>
            <input
              type="file"
              id="resumeUpload"
              @change="handleFileUpload"
              accept=".pdf,.doc,.docx"
            />
          </span>
        </fieldset>

        <span>
          <label for="termsAccepted">
            <input
              type="checkbox"
              id="termsAccepted"
              v-model="formdata.termsAccepted"
            />
            I accept the terms and conditions
          </label>
        </span>

        <button type="submit" :disabled="!formdata.termsAccepted">
          Submit
        </button>
      </form>
    </div>
  </main>
</template>

<script setup lang="ts">
import { reactive } from "vue";

type FormData = {
  fullName: string;
  email: string;
  phoneNumber: string;
  gender: string;
  skills: string[];
  experienceLevel: string;
  resumeUpload: File | null;
  coverLetter: string;
  termsAccepted: boolean;
};

const formdata = reactive<FormData>({
  fullName: "",
  email: "",
  phoneNumber: "",
  gender: "",
  skills: [],
  experienceLevel: "",
  coverLetter: "",
  resumeUpload: null,
  termsAccepted: false,
});

function handleFileUpload(event: Event) {
  const target = event.target as HTMLInputElement;
  formdata.resumeUpload = target.files ? target.files[0] : null;
}

function handleSubmit() {
  // Log the reactive formdata object directly for accurate values
  console.log({
    ...formdata,
    resumeUpload: formdata.resumeUpload?.name || null,
  });
}
</script>

<style scoped>
@reference "tailwindcss";
form {
  @apply flex flex-col gap-4 p-6 bg-gray-100 rounded-lg shadow-md;
}

fieldset {
  @apply border border-gray-300 p-4 rounded-lg flex flex-col gap-4;
}

.prof-info span {
  @apply flex flex-col gap-2 items-start;
}

input,
textarea,
select {
  @apply p-1 border border-gray-300 rounded-md;
}

button {
  @apply bg-blue-500 text-white p-2 rounded-md hover:bg-blue-600 disabled:opacity-50 cursor-pointer;
}

.personal-info span {
  @apply flex items-center gap-2;
}

#skills label {
  @apply cursor-pointer;
}
</style>

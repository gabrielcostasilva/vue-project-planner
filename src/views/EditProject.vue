<template>
  <form @submit.prevent="handleUpdate">
    <label>Title</label>
    <input type="text" v-model="title" required />
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";

export default {
  props: ["id"],
  setup(props) {
    const title = ref("");
    const details = ref("");

    const uri = `http://localhost:3000/projects/${props.id}`;

    const router = useRouter();

    const handleUpdate = () => {
      fetch(uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: title.value,
          details: details.value,
        }),
      })
        .then(() => router.push("/"))
        .catch((err) => console.log(err));
    };

    onMounted(() => {
      fetch(uri)
        .then((res) => res.json())
        .then((data) => {
          (title.value = data.title), (details.value = data.details);
        });
    });

    return { title, details, handleUpdate };
  },
};
</script>

<style>
</style>
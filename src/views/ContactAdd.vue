<template>
  <div class="page">
    <h4>Thêm Liên hệ Mới</h4>
    <ContactForm :contact="contact" @submit:contact="createContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import ContactService from '@/services/contact.service';

export default {
  components: {
    ContactForm,
  },

  data() {
    return {
      contact: {
        name: '',
        email: '',
        phone: '',
      },
      message: '',
    };
  },

  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data);
        alert('Liên hệ được tạo thành công.');
        this.$router.push({ name: 'contactbook' });
      } catch (error) {
        console.log(error);
        this.message = 'Đã xảy ra lỗi khi tạo liên hệ.';
      }
    },
  },
};
</script>

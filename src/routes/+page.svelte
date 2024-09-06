<script>
  import Button from "../lib/button.svelte";
  import Checkbox from "../lib/checkbox.svelte";
  import Input from "../lib/input.svelte";
  import Modal from "../lib/modal.svelte";

  let name = "";
  let company = "";
  let email = "";
  let phone = "";
  let subject = "";
  let message = "";
  let consent = false;

  let formErrors = {
    name: "",
    company: "",
    email: "",
    phone: "",
    message: "",
    consent: "",
  };

  let showModal = false;
  let modalMessage = "";

  const validateEmail = (email) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);

  const validatePhone = (phone) => /^\d+$/.test(phone);

  const validateForm = () => {
    formErrors = {};

    if (!name) formErrors.name = "Имя обязательно";
    if (!company) formErrors.company = "Компания обязательна";
    if (!email || !validateEmail(email))
      formErrors.email = "Введите корректный email";
    if (phone && !validatePhone(phone))
      formErrors.phone = "Введите корректный телефон";
    if (!message) formErrors.message = "Сообщение обязательно";
    if (!consent) formErrors.consent = "Требуется согласие";

    return Object.keys(formErrors).length === 0;
  };

  const clearError = (field) => {
    formErrors = { ...formErrors, [field]: "" };
  };

  const handleSubmit = () => {
    if (validateForm()) {
      modalMessage = "The form has been successfully submitted";
      showModal = true;
      name = "";
      company = "";
      email = "";
      phone = "";
      subject = "";
      message = "";
      consent = false;
    }
  };

  const closeModal = () => {
    showModal = false;
  };
</script>

<div class="container">
  <h1>Hello</h1>
  <div class="form-block">
    <h2>For business enquiries please <br /> use the form below</h2>
    <p>*Required</p>
    <div class="inputs">
      <Input
        label="Name"
        type="text"
        bind:value={name}
        on:input={() => clearError("name")}
        error={formErrors.name}
      />

      <Input
        label="Company"
        type="text"
        bind:value={company}
        on:input={() => clearError("company")}
        error={formErrors.company}
      />

      <Input
        label="Email"
        type="email"
        bind:value={email}
        on:input={() => clearError("email")}
        error={formErrors.email}
      />

      <Input
        label="Phone"
        type="tel"
        bind:value={phone}
        on:input={() => clearError("phone")}
        error={formErrors.phone}
      />

      <Input label="Subject" type="text" bind:value={subject} />

      <Input
        label="Message"
        type="textarea"
        bind:value={message}
        on:input={() => clearError("message")}
        error={formErrors.message}
      />

      <div class="checkbox-group">
        <Checkbox
          label="I accept"
          bind:checked={consent}
          on:change={() => clearError("consent")}
        />
        <p>I accept <a href="#">Terms and Privacy Policy</a></p>
      </div>
      {#if formErrors.consent}
        <p class="error">{formErrors.consent}*</p>
      {/if}

      <div class="submit-button">
        <Button onClick={handleSubmit} color="#2C2F47" />
      </div>
    </div>
  </div>

  <Modal message={modalMessage} show={showModal} onClose={closeModal} />
</div>

<style>
  .container {
    width: 100%;
    height: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: url(../img/back.jpg) no-repeat center center;
    background-size: cover;
    flex-direction: column;
    color: white;
  }
  .form-block {
    background-color: #171929;
    border-radius: 27px;
    padding: 30px;
    margin: 0 20px;
  }
  .form-block h2 {
    text-align: center;
    font-size: 18px;
    font-weight: 300;
  }
  .form-block p {
    font-size: 12px;
    font-weight: 400;
    text-align: center;
    color: #797ea3;
  }
  .inputs a {
    color: #8f94bf;
  }

  .checkbox-group {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;
  }
  .submit-button {
    display: flex;
    justify-content: center;
    margin-top: 10px;
  }
  .error {
    font-size: 10px;
    color: rgb(178, 24, 24);
  }
</style>

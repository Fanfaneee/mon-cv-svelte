<script>
  // Plus besoin d'import !
  // On définit "onRemove" comme une propriété que le parent doit fournir
  let { exp = $bindable(), onRemove } = $props();

  function handleRemove() {
    onRemove(exp.id);
  }
</script>

<div class="exp-card">
  <div class="field">
    <label for="company-{exp.id}">Entreprise</label>
    <input
      id="company-{exp.id}"
      placeholder="Ex: Google"
      bind:value={exp.company}
    />
  </div>

  <div class="field">
    <label for="role-{exp.id}">Poste</label>
    <input
      id="role-{exp.id}"
      placeholder="Ex: Développeur"
      bind:value={exp.role}
    />
  </div>

  <div class="field">
    <label for="year-{exp.id}">Année</label>
    <input id="year-{exp.id}" placeholder="Ex: 2023" bind:value={exp.year} />
  </div>

  <button onclick={handleRemove} type="button" class="btn-delete">
    Retirer
  </button>
</div>

<style>
  .exp-card {
    border: 1px solid #e0e0e0;
    padding: 15px;
    margin: 0 auto 15px auto;
    border-radius: 8px;
    background: #fafafa;
    width: 75%;
  }
  .field {
    margin-bottom: 10px;
  }
  label {
    display: block;
    font-weight: bold;
    font-size: 0.8rem;
    margin-bottom: 4px;
  }
  input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  .btn-delete {
    background: #ff4d4d;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 4px;
    cursor: pointer;
  }
</style>

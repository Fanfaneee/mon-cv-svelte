<script>
  import ExperienceForm from "./ExperienceForm.svelte";

  let name = "Jean Dupont";
  let job = "Développeur Fullstack";

  // IDs en string pour éviter les conflits avec randomUUID()
  let experiences = [
    { id: "1", company: "Google", role: "Stagiaire", year: "2023" },
  ];

  function addExp() {
    experiences = [
      ...experiences,
      { id: crypto.randomUUID(), company: "", role: "", year: "" },
    ];
  }

  function removeExp(id) {
    experiences = experiences.filter((e) => e.id !== id);
  }
</script>

<main>
  <section class="editor">
    <h2>📝 Éditeur</h2>

    <div class="field">
      <label for="full-name">Nom Complet</label>
      <input id="full-name" type="text" bind:value={name} />
    </div>

    <div class="field">
      <label for="job-title">Poste visé</label>
      <input id="job-title" type="text" bind:value={job} />
    </div>

    <h3>Expériences</h3>
    {#each experiences as exp (exp.id)}
      <ExperienceForm bind:exp onRemove={removeExp} />
    {/each}

    <button onclick={addExp} class="btn-add">+ Ajouter</button>
  </section>

  <section class="preview">
    <div class="cv-paper">
      <header>
        <h1>{name || "Votre Nom"}</h1>
        <p class="subtitle">{job || "Votre Poste"}</p>
      </header>

      <div class="content">
        <h3>Parcours professionnel</h3>
        {#each experiences as exp (exp.id)}
          <div class="item">
            <strong>{exp.year || "Année"}</strong> —
            {exp.role || "Poste"} chez <em>{exp.company || "Entreprise"}</em>
          </div>
        {:else}
          <p>Aucune expérience listée.</p>
        {/each}
      </div>
    </div>
  </section>
</main>

<style>
  :global(html) {
    box-sizing: border-box;
    font-family: sans-serif;
  }
  :global(*, *::before, *::after) {
    box-sizing: inherit;
  }

  main {
    display: grid;
    grid-template-columns: 400px 1fr;
    height: 100vh;
  }

  .editor {
    padding: 20px;
    background: white;
    border-right: 1px solid #ddd;
    overflow-y: auto;
  }

  .preview {
    padding: 40px;
    background: #f0f2f5;
    display: flex;
    justify-content: center;
    overflow-y: auto;
  }

  .cv-paper {
    width: 210mm;
    min-height: 297mm;
    background: white;
    padding: 50px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  }

  .field {
    margin-bottom: 15px;
  }
  label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
  }
  input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  .btn-add {
    width: 100%;
    background: #4a90e2;
    color: white;
    border: none;
    padding: 12px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }

  .item {
    margin-bottom: 15px;
    border-left: 3px solid #4a90e2;
    padding-left: 10px;
  }

  @media print {
    .editor {
      display: none;
    }
    main {
      grid-template-columns: 1fr;
    }
    .preview {
      padding: 0;
      background: white;
    }
    .cv-paper {
      box-shadow: none;
      width: 100%;
    }
  }
</style>

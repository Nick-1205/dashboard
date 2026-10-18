<script>
  import { aufgaben } from "../Speicher/stores";
  import ListeAPI from "../Speicher/ListeAPI";
  import { v4 as uuidv4 } from "uuid";

  let titel = "";
  let inhalt = "";
  let formularSichtbar = "";

  export const formularAnzeigen = () => {
    formularSichtbar = "is-active";
  };

  const schließen = () => {
    formularSichtbar = "";
  };

  const speicherFormular = () => {
    if (titel.trim() === "" || inhalt.trim() === "") {
      return;
    }
    $aufgaben = [
      {
        id: uuidv4(),
        titel: titel,
        inhalt: inhalt,
        erledigt: false,
      },
      ...$aufgaben,
    ];
    console.log($aufgaben);
    ListeAPI.speichern($aufgaben);
    titel = "";
    inhalt = "";
    formularSichtbar = "";
  };
</script>

<div class="modal {formularSichtbar}">
  <div class="modal-background">
    <div class="modal-content">
      <div class="box">
        <form on:submit|preventDefault={speicherFormular}>
          <div class="field">
            <div class="control">
              <input
                class="input"
                type="text"
                placeholder="Titel"
                bind:value={titel}
              />
            </div>
          </div>
          <div class="field">
            <div class="control">
              <textarea
                class="textarea"
                placeholder="Inhalt"
                bind:value={inhalt}
              ></textarea>
            </div>
          </div>
          <div class="field is-grouped">
            <div class="control">
              <button type="submit" class="button is-primary">Speichern</button>
            </div>
            <div class="control">
              <button on:click={schließen} class="button is-danger"
                >Abbrechen</button
              >
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
  <button on:click={schließen} class="modal-close is-large" aria-label="close"
  ></button>
</div>

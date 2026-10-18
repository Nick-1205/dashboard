<script>
  import "../node_modules/bulma/css/bulma.min.css";
  import Navbar from "./Komponenten/Navbar.svelte";
  import { aufgaben } from "./Speicher/stores";
  import Tabelle from "./Komponenten/Tabelle.svelte";
  import Liste from "./Komponenten/Liste.svelte";
  import Router from "svelte-spa-router";
  import ListeAPI from "./Speicher/ListeAPI";
  import { onMount } from "svelte";

  onMount(async () => {
    $aufgaben = await ListeAPI.laden();
  });

  $: aufgabenAnzahl = $aufgaben.length;
  $: aufgabenAnzahlErledigt = $aufgaben.filter(
    (aufgabe) => aufgabe.erledigt,
  ).length;
</script>

<svelte:head
  ><title>Board: {aufgabenAnzahlErledigt}/{aufgabenAnzahl}</title></svelte:head
>

<Navbar>To-do Liste: {aufgabenAnzahlErledigt}/{aufgabenAnzahl}</Navbar>

<Router
  routes={{
    "/": Liste,
    "/tabelle": Tabelle,
  }}
></Router>

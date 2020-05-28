<template>
  <b-container class="text-left">
    <b-row align-h="start">
      <b-col cols="12" class="m-1">
        <h3>Impress Narrative</h3>
      </b-col>
    </b-row>

    <b-row >

      <b-col cols="12">
        <b-card
          title="Narrator:"
          img-top
          tag="article"
          style="max-width: 100%"
          class="m-1"
        >
          <b-card-text id="narratorText">
            Narrator text
          </b-card-text>
        </b-card>

      </b-col>

    </b-row>

    <!-- Game Events -->
    <b-row >
      <b-col cols="12">
        <b-card
          title="Game Events:"
          img-top
          tag="article"
          style="max-width: 100%"
          class="m-1"
        >
          <b-button href="#" id="game_start" class="m-1">Start Game</b-button>
          <b-button href="#" id="game_continue"  class="m-1">Continue Game</b-button>
          <b-button href="#" id="game_win" class="m-1">Win Game</b-button>
          <b-button href="#" id="game_loss" class="m-1">Lose Game</b-button>
          <b-button href="#" id="game_stop" class="m-1">Stop Game</b-button>
        </b-card>
      </b-col>
    </b-row>

    <!-- World Events -->
    <b-row >
      <b-col cols="12">
        <b-card
          title="World Events:"
          img-top
          tag="article"
          style="max-width: 100%"
          class="m-1"
        >
          <b-button href="#" id="world_start" class="m-1">Start World</b-button>
          <b-button href="#" id="world_continue"  class="m-1">Continue World</b-button>
          <b-button href="#" id="world_complete" class="m-1">Complete World</b-button>
        </b-card>
      </b-col>
    </b-row>

    <!-- Level Events -->
    <b-row >
      <b-col cols="12">
        <b-card
          title="Level Events:"
          img-top
          tag="article"
          style="max-width: 100%"
          class="m-1"
        >
          <b-button href="#" id="level_start" class="m-1">Start Level</b-button>
          <b-button href="#" id="level_continue"  class="m-1">Continue Level</b-button>
          <b-button href="#" id="level_win" class="m-1">Win Level</b-button>
          <b-button href="#" id="level_loss" class="m-1">Lose Level</b-button>
        </b-card>
      </b-col>
    </b-row>

    <!-- Action Events -->
    <b-row >
      <b-col cols="12">
        <b-card
          title="Action Events:"
          img-top
          tag="article"
          style="max-width: 100%"
          class="m-1"
        >
          <b-button href="#" id="action_attempt" class="m-1">Attempt Action</b-button>
          <b-button href="#" id="action_success"  class="m-1">Succeed at Action</b-button>
          <b-button href="#" id="action_fail" class="m-1">Fail at Action</b-button>
        </b-card>
      </b-col>
    </b-row>

    <!-- <b-row>
      <b-col  class="m-1">
        <b-button href="#" id="perceive" class="m-1">Post Perceive</b-button>
        <b-button href="#" id="utterance" class="m-1">Get Utterance</b-button>
      </b-col>
    </b-row> -->

  </b-container>

</template>

<script>
  import JQuery from 'jquery'
  let $ = JQuery
  export default {
    name: 'ImpressNarrative',
  }

  function getUtterance() {
    $.get("http://localhost:1337/localhost:5000/decide?c=Narrator").done(function( data ) {
      $("#narratorText").text(data[0].Utterance)
    });
  }

  function getEventUtterance(event) {
    $.post("http://localhost:1337/localhost:5000/perceive?c=Narrator",
      JSON.stringify([
          "event(property-change, world, DialogueState(Player)," + event + ")"
        ])
    ).then(getUtterance());
  }

  $(document).ready(function() {

    getUtterance();

    // Game Events
    $("#game_start").click(function(){
      getEventUtterance("GAME_START");
    });

    $("#game_continue").click(function(){
      getEventUtterance("GAME_CONTINUE");
    });

    $("#game_win").click(function(){
      getEventUtterance("GAME_WIN");
    });

    $("#game_loss").click(function(){
      getEventUtterance("GAME_LOSS");
    });

    $("#game_stop").click(function(){
      getEventUtterance("GAME_NOT_STARTED");
    });


    // World Events
    $("#world_start").click(function(){
      getEventUtterance("WORLD_START");
    });

    $("#world_continue").click(function(){
      getEventUtterance("WORLD_CONTINUE");
    });

    $("#world_complete").click(function(){
      getEventUtterance("WORLD_COMPLETE");
    });


    // Level Events
    $("#level_start").click(function(){
      getEventUtterance("LEVEL_START");
    });

    $("#level_continue").click(function(){
      getEventUtterance("LEVEL_CONTINUE");
    });

    $("#level_win").click(function(){
      getEventUtterance("LEVEL_WIN");
    });

    $("#level_loss").click(function(){
      getEventUtterance("LEVEL_LOSS");
    });


    // Action Events
    $("#action_attempt").click(function(){
      getEventUtterance("ACTION_ATTEMPT");
    });

    $("#action_fail").click(function(){
      getEventUtterance("ACTION_FAIL");
    });

    $("#action_success").click(function(){
      getEventUtterance("ACTION_SUCCESS");
    });

    // $("#perceive").click(function(){
    //   $.post("http://localhost:1337/localhost:5000/perceive?c=Narrator",
    //     JSON.stringify([
    //         "event(property-change, world, DialogueState(Player), GAME_START)"
    //       ])
    //   );
    // });
    //
    // $("#utterance").click(function(){
    //   $.get("http://localhost:1337/localhost:5000/decide?c=Narrator").done(function( data ) {
    //     // alert( "Data Loaded: " + data[0].Utterance );
    //     $("#narratorText").text(data[0].Utterance)
    //   });
    // });

  });
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }

  /* <b-button size="sm" @click="toggle">
    {{ show ? 'Hide' : 'Show' }} Alert
  </b-button> */

</style>

<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./components/Tabs.svelte";
  import PollList from "./components/PollList.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";

  // tabs
  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";

  const tabChange = (e) => {
    activeItem = e.detail;
  };

  // polls
  let polls = [
    {
      id: 1,
      question: "React or Angular",
      answerA: "React",
      answerB: "Angular",
      votesA: 15,
      votesB: 9,
    },
    {
      id: 2,
      question: "Ice Cream or Chocolate",
      answerA: "Ice Cream",
      answerB: "Chocolate",
      votesA: 5,
      votesB: 11,
    },
  ];

  // handle vote
  const handleVote = (e) => {
    const { option, id } = e.detail;

    let copiedPolls = [...polls];
    let upvotedPoll = copiedPolls.find((poll) => poll.id === id);

    if (option === "a") {
      upvotedPoll.votesA++;
    }

    if (option === "b") {
      upvotedPoll.votesB++;
    }

    polls = copiedPolls;
  };

  // handle delete
  const handleDelete = (e) => {
    const id = e.detail;
    polls = polls.filter((poll) => poll.id !== id);
  };

  // handle add
  const handleAdd = (e) => {
    const poll = e.detail;
    polls = [poll, ...polls];

    activeItem = "Current Polls";
  };
</script>

<Header />
<main>
  <Tabs {items} {activeItem} on:tabChange={tabChange} />
  {#if activeItem === "Current Polls"}
    <PollList {polls} on:vote={handleVote} on:delete={handleDelete} />
  {:else}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

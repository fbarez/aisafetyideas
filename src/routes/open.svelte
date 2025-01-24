<script>
  import Nav from "$lib/Nav.svelte";
  import Footer from "$lib/Footer.svelte";
  import { onMount } from "svelte";
  import tippy from "sveltejs-tippy";
  import { getTable } from "$lib/db";
  import SvelteHeatmap from "svelte-heatmap";
  import moment from "moment";

  let ideas = [],
    comments = [],
    users = [],
    likes = [];

  onMount(async () => {
    [ideas, comments, users, likes] = await Promise.all([
      getTable("ideas"),
      getTable("comments"),
      getTable("users"),
      getTable("idea_user_likes"),
    ]);
  });
</script>

<svelte:head>
  <title>Open data | AI safety ideas</title>
</svelte:head>

<Nav />
<div class="w-container">
  <h2>About</h2>
  <p class="team">
    The AI Safety Ideas platform is a public Apart tool used for collecting research in AI safety, collaborate on projects, and facilitate mentorship.
  </p>
  <h2>Team</h2>
  <p class="team">
    The <a href="https://apartresearch.com">Apart Research</a> team, we have
    multiple volunteers and collaborators that have joined on our
    <a href="https://apartresearch.com/join">Discord</a> and in our other projects.
  </p>
  <div class="members">
    <div class="member">
      <img
        src="https://media-exp2.licdn.com/dms/image/C5603AQGtXh8ofQbCOA/profile-displayphoto-shrink_800_800/0/1651368132506?e=1660176000&v=beta&t=Gai4wfy_Fs8hPXf1AcEtNiQpyRVX2Pewo4fOLFPqKRI"
        alt="Team member esben"
      />
      <h3>Esben Kran</h3>
      <p>
        Founder,
        <a href="mailto:esben@apartresearch.com" class="contact">contact</a>
      </p>
    </div>
    <div class="member">
      <img
        src="https://media-exp2.licdn.com/dms/image/C4D03AQHrBuBZUh-xfQ/profile-displayphoto-shrink_800_800/0/1649782705603?e=1660176000&v=beta&t=h6LohAJclafKsA8vkxTdtyNqhl_EvARl9Bezl1dbK10"
        alt="Team member Jonathan"
      />
      <h3>Jonathan H. Rystrøm</h3>
      <p>
        Co-lead,
        <a href="mailto:jonathan@apartresearch.com" class="contact">contact</a>
      </p>
    </div>
    <div class="member">
      <img
        src="https://sala.ai/images/img0001-copy-p-500.png"
        alt="Team member Maris"
      />
      <h3>Maris Sala</h3>
      <p>
        Collaborator, <a href="https://sala.ai" class="contact">contact</a>
      </p>
    </div>
    <div class="member">
      <img
        src="https://fbarez.github.io/images/fb2017.jpg"
        alt="team member Fazl"
      />
      <h3>Fazl Barez</h3>
      <p>
        Collaborator & Advisor, <a
          href="https://fbarez.github.io/"
          class="contact">contact</a
        >
      </p>
    </div>
  </div>
  <h2>Open impact metrics of AIS&nbsp;Safety Ideas</h2>
  <p>
    The AI safety research ideas platform commits to transparency and sharing
    our metrics. We hope this enables easier evaluation of the platform's
    impact. Read the <a
      href="http://forum.effectivealtruism.org/posts/nxeL7XFvtQCx7hpxo/everyone-show-us-your-numbers"
      target="_blank"
      rel="noopener noreferrer"
    >
      forum post
    </a> for more details.
  </p>
  <h2 id="metrics">Metrics</h2>
  <p class="metrics-text">
    Apart Research has <span
      use:tippy={{
        content:
          "Apart Research funding from the FTX Future Fund regrantor program.",
      }}
      class="inline-number">$95,000</span
    >
    in funding. On <a href="/">aisafetyideas.com</a>, the total number of ideas
    is
    <span
      class="inline-number"
      use:tippy={{
        content: "The total number of ideas on the site.",
      }}
    >
      {ideas.length}
    </span>
    with
    <span
      class="inline-number"
      use:tippy={{
        content: "Total comments on the site.",
      }}>{comments.length}</span
    >
    total comments of which
    <span
      class="inline-number"
      use:tippy={{
        content: "Total replies on the site.",
      }}
    >
      {comments.filter((com) => com.reply_to).length}
    </span>
    are replies. Of all ideas,
    <span
      class="inline-number"
      use:tippy={{
        content: "Expert verified ideas.",
      }}>{ideas.filter((idea) => idea.verified).length}</span
    >
    are verified by expert profiles and
    <span
      class="inline-number"
      use:tippy={{
        content: "Ideas filtered by the Apart Research team.",
      }}>{ideas.filter((idea) => idea.filtered).length}</span
    >
    are filtered by the Apart Research team and they have been liked a total of
    <span
      class="inline-number"
      use:tippy={{
        content: "Total amount of likes of ideas on the site.",
      }}>{likes.length}</span
    >
    times. The total number of users is
    <span
      class="inline-number"
      use:tippy={{
        content: "Total amount of users on the site.",
      }}
    >
      {users.length}
    </span>
    and the number of expert users is
    <span
      class="inline-number"
      use:tippy={{
        content:
          "Total number of expert users, i.e. users who are experts within a specific category.",
      }}>{users.filter((user) => user.expert).length}</span
    >.
    <span
      class="inline-number"
      use:tippy={{ content: "The amount of user interviews for the site." }}
    >
      18
    </span>
    user interviews have been done. The current salary for core employees is
    <span
      class="inline-number"
      use:tippy={{ content: "Salary for core employees per year." }}
      >$60,000</span
    >.
  </p>

  <h3 id="commits">Website updates by day</h3>
  <div class="open-day-block" id="commit-map">
    <SvelteHeatmap
      data={[
        { date: "2022-04-16", value: 1 },
        { date: "2022-04-19", value: 1 },
        { date: "2022-04-20", value: 1 },
        { date: "2022-04-21", value: 1 },
        { date: "2022-04-22", value: 1 },
        { date: "2022-04-23", value: 1 },
        { date: "2022-04-24", value: 1 },
        { date: "2022-04-26", value: 1 },
        { date: "2022-04-27", value: 1 },
        { date: "2022-04-28", value: 1 },
        { date: "2022-04-29", value: 1 },
        { date: "2022-04-30", value: 1 },
        { date: "2022-05-15", value: 1 },
        { date: "2022-05-17", value: 1 },
        { date: "2022-05-18", value: 1 },
        { date: "2022-05-19", value: 1 },
        { date: "2022-05-20", value: 1 },
        { date: "2022-05-21", value: 1 },
        { date: "2022-05-23", value: 1 },
        { date: "2022-05-24", value: 1 },
        { date: "2022-05-25", value: 1 },
        { date: "2022-05-26", value: 1 },
        { date: "2022-05-27", value: 1 },
        { date: "2022-05-30", value: 1 },
        { date: "2022-05-31", value: 1 },
        { date: "2022-06-01", value: 1 },
        { date: "2022-06-02", value: 1 },
        { date: "2022-06-03", value: 1 },
        { date: "2022-06-05", value: 1 },
        { date: "2022-06-06", value: 1 },
        { date: "2022-06-07", value: 1 },
        { date: "2022-06-08", value: 1 },
        { date: "2022-06-09", value: 1 },
        { date: "2022-06-10", value: 1 },
        { date: "2022-06-11", value: 1 },
        { date: "2022-06-12", value: 1 },
        { date: "2022-06-13", value: 1 },
        { date: "2022-06-14", value: 1 },
        { date: "2022-06-16", value: 1 },
        { date: "2022-06-17", value: 1 },
        { date: "2022-06-19", value: 1 },
        { date: "2022-06-20", value: 1 },
        { date: "2022-06-21", value: 1 },
        { date: "2022-06-22", value: 1 },
        { date: "2022-06-24", value: 1 },
        { date: "2022-06-25", value: 1 },
        { date: "2022-06-26", value: 1 },
        { date: "2022-06-27", value: 1 },
        { date: "2022-06-28", value: 1 },
        { date: "2022-06-29", value: 1 },
        { date: "2022-06-30", value: 1 },
        { date: "2022-07-1", value: 1 },
        { date: "2022-07-2", value: 1 },
        { date: "2022-07-3", value: 1 },
        { date: "2022-07-5", value: 1 },
        { date: "2022-07-7", value: 1 },
        { date: "2022-07-8", value: 1 },
      ]}
      endDate={moment().toDate()}
      startDate={moment("2022-04-15").toDate()}
      view="yearly"
      colors={["#44FF98"]}
      emptyColor={"#DAFFEA"}
    />
  </div>
  <h3>Website visitors</h3>
  <div class="open-graph-wrapper">
    <div class="w-embed w-iframe">
      <iframe
        width="100%"
        height="475px"
        src="https://datastudio.google.com/embed/reporting/70009ccf-f7f2-457f-bc8f-ef9dbbd6ed65/page/DbGrC"
        frameborder="0"
        style="border:0"
        allowfullscreen=""
        title="Website visitors"
      />
    </div>
  </div>
  <!-- <h2 id="roadmap">Feature roadmap</h2>
  <div class="timeline-wrapper">
    <div class="timeline-block past">
      <h3 class="list-idea-header">Version 0.1</h3>
      <p class="list-idea-summary">
        The first version was <a
          href="https://docs.google.com/spreadsheets/u/2/d/1Ep8Dd52c00kxWvu75btazHEdPSA7jVJwrY51jKfPSBo/edit#gid=719912604"
          target="_blank">this spreadsheet.</a
        >
      </p>
    </div>
    <div class="timeline-pointer">👉🏼</div>
    <div class="timeline-block past">
      <h3 class="list-idea-header">Version 0.2</h3>
      <p class="list-idea-summary">
        A list of ideas on a website designed for the purpose. Include links to
        more info.
      </p>
    </div>
    <div class="timeline-pointer">👉🏼</div>
    <div class="timeline-block">
      <h3 class="list-idea-header">Version 0.3</h3>
      <p class="list-idea-summary">
        Add active RFPs as links. Upvoting and sharing of ideas. Make ideas
        "shovel-ready".
      </p>
    </div>
    <div class="timeline-pointer">👉🏼</div>
    <div class="timeline-block">
      <h3 class="list-idea-header">Version 0.4</h3>
      <p class="list-idea-summary">
        Showcasing upvotes on ideas, enabling bounties and RFPs.
      </p>
    </div>
    <div class="timeline-pointer">👉🏼</div>
    <div class="timeline-block">
      <h3 class="list-idea-header">Version 0.5</h3>
      <p class="list-idea-summary">
        Adding comments to ideas. Possibly integrated with the AF&nbsp;comment
        system.
      </p>
    </div>
    <div class="timeline-pointer">👉🏼</div>
    <div class="timeline-block">
      <h3 class="list-idea-header">Version 0.6</h3>
      <p class="list-idea-summary">
        Profiles implemented e.g. from LW. Add idea categories. Profile pages.
      </p>
    </div>
    <div class="timeline-pointer">👉🏼</div>
    <div class="timeline-block">
      <h3 class="list-idea-header">Version 0.7</h3>
      <p class="list-idea-summary">
        Create a networked incentive system for mentorship. Any ideas here are
        appreciated.
      </p>
    </div>
  </div> -->
</div>
<Footer />

<style>
  .members {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: left;
    align-items: flex-start;
    column-gap: 1rem;
    row-gap: 1rem;
  }

  .member {
    display: flex;
    flex-direction: column;
    max-width: 15rem;
    padding: 0.9rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }

  .member > img {
    width: 100%;
    border-radius: 0.5rem;
    filter: grayscale(10%);
  }

  .member > h3 {
    margin-top: 1rem;
    margin-bottom: 0rem;
  }

  .member > p {
    margin: 0;
  }

  .metrics-text {
    font-size: 1rem;
    line-height: 1.75rem;
  }

  .inline-number {
    display: inline-block;
    line-height: 1rem;
    text-align: center;
    padding: 0.1rem 0.3rem;
    margin: 0 0.1rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    font-style: bold;
    transition: 0.2s ease-in-out transform, 0.2s ease-in-out background-color;
    cursor: cell;
  }

  .inline-number:hover {
    transform: translate(0, -0.1rem);
    background-color: #eee;
  }

  .w-container {
    margin: 0 auto;
    padding: 0 0.5rem;
  }

  /* Mobile */
  @media only screen and (max-width: 600px) {
    .open-block {
      width: 100%;
      margin-bottom: 20px;
    }

    .members {
      justify-content: center;
    }

    .timeline-block {
      width: 100%;
    }

    .timeline-pointer {
      display: none;
    }
  }
</style>

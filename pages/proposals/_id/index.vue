<template>
  <div>
    <div class="mb-2"><nuxt-link to="/proposals" class="is-size-7">&lt; All Proposals</nuxt-link></div>
    <div v-if="loading">Loading Proposal..</div>
    <div v-else-if="proposal" class="columns">
      <div class="column is-two-thirds">
        <div class="title is-4">{{proposal.title}}</div>
        <div class="subtitle"><span class="tag" :class="{'is-success': proposal.status == 'ACTIVE', 'is-warning': proposal.status == 'DRAFT', 'is-link': proposal.status == 'PENDING'}">{{ proposal.status }}</span></div>
        <small>
          <p>Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, "Lorem ipsum dolor sit amet..", comes from a line in section 1.10.32.</p>
          <p>The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from "de Finibus Bonorum et Malorum" by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham.</p>
        </small>
        <div class="box mt-5">
          <h5 class="box-title">Cast your vote</h5>
          <div>
            <button class="button is-primary is-fullwidth">Vote</button>
          </div>
        </div>
        <div class="box mt-5">
          <h5 class="box-title">Votes</h5>
        </div>
      </div>
      <div class="column">
        <div class="box">
          <h5 class="box-title">Information</h5>
          <div>by <nuxt-link :to="'/account/'+proposal.account"><b>{{proposal.account}}</b></nuxt-link></div>
          <div>created {{ $moment(proposal.created+"Z").fromNow() }}</div>
        </div>
        <div class="box">
          <h5 class="box-title">Results</h5>
        </div>
      </div>
    </div>
    <h4 v-else class="has-text-centered">Could not retrieve proposal</h4>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      proposal: null,
      id: this.$route.params.id
    }
  },

  created () {
    this.getProposal(this.id)
  },

  methods: {
    async getProposal (id) {
      this.loading = true
      try {
        await new Promise(resolve => setTimeout(resolve, 1000))
        this.proposal = {
          id: 4,
          title: 'Change to Rebase Sell percentage',
          account: 'extemporized',
          created: '11-11-2020',
          status: 'DRAFT'
        }
      } catch (e) {
        console.log(e)
      }
      this.loading = false
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
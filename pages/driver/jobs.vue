<template>
  <div class="page-driver-jobs section_mod-2">
    <h1 class="ui-title-page">Jobs</h1>
    <div class="triagl triagl-btm"></div>
    <div class="empty-space pb-5">
      <div class="pb-5"></div>
    </div>
    <b-container>
      <Calendar :events="events" />
    </b-container>

    <b-container>
      <!-- Modal -->
      <div v-if="Object.keys(driverJobsObject).length">
        <b-modal
          v-for="job in driverJobsObject"
          :id="job.id.toString()"
          :key="job.id"
          size="xl"
          scrollable
          hide-footer
          title="Job Info"
        >
          <b-row>
            <b-col>
              <div class="card mt-3 section_mod-2">
                <div class="card-body">
                  <b-row>
                    <b-col xl="4">
                      <h2 class="ui-title-block">
                        <div
                          v-for="job_meta in job.job_metas"
                          :key="job_meta.index"
                        >
                          <div v-if="job_meta.key === 'movingDate'">
                            <fa :icon="['fas', 'calendar']" />
                            {{ job_meta.value | isoDateToString }}
                          </div>
                        </div>
                      </h2>
                      <div class="border-color border-color_default"></div>
                      <div class="customer-info">
                        <h4>Customer info:</h4>
                        <div
                          v-for="job_meta in job.job_metas"
                          :key="job_meta.index"
                        >
                          <div v-if="job_meta.key === 'customerInfoName'">
                            Name: {{ job_meta.value }}
                          </div>
                          <div v-if="job_meta.key === 'customerInfoEmail'">
                            Email: {{ job_meta.value }}
                          </div>
                          <div v-if="job_meta.key === 'customerInfoPhone'">
                            Phone: {{ job_meta.value }}
                          </div>
                        </div>
                      </div>
                    </b-col>
                    <b-col xl="4">
                      <div
                        v-for="job_meta in job.job_metas"
                        :key="job_meta.index"
                      >
                        <div v-if="job_meta.key === 'collection'">
                          <h4>Addresses:</h4>
                          <h5>Collection:</h5>
                          <p>Postcode: {{ job_meta.value.postcode }}</p>
                          <p>Address: {{ job_meta.value.address }}</p>
                          <p>City: {{ job_meta.value.city }}</p>
                        </div>
                        <div v-if="job_meta.key === 'delivery'">
                          <h5>Delivery:</h5>
                          <p>Postcode: {{ job_meta.value.postcode }}</p>
                          <p>Address: {{ job_meta.value.address }}</p>
                          <p>City: {{ job_meta.value.city }}</p>
                        </div>
                        <div
                          v-if="
                            job_meta.key === 'waypoints' &&
                              job_meta.value.length > 0
                          "
                        >
                          <h5>Stops:</h5>
                          <div
                            v-for="waypoint in job_meta.value"
                            :key="waypoint.index"
                          >
                            <p>Postcode: {{ waypoint.postcode }}</p>
                            <p>Address: {{ waypoint.address }}</p>
                            <p>City: {{ waypoint.city }}</p>
                            <hr />
                          </div>
                        </div>
                      </div>
                    </b-col>
                    <b-col xl="4">
                      <div
                        v-for="job_meta in job.job_metas"
                        :key="job_meta.index"
                      >
                        <div v-if="job_meta.key === 'vanSize'">
                          <h4>Others info:</h4>

                          <p>Van Size: {{ job_meta.value | vanSize }}</p>
                        </div>
                        <div v-if="job_meta.key === 'helpersRequired'">
                          <p>
                            Helpers Required:
                            {{ job_meta.value | helpersRequired }}
                          </p>
                        </div>
                        <div v-if="job_meta.key === 'additionalTimePrice'">
                          <p>
                            Additional Time Price:
                            {{ job_meta.value | currency }} per half hour
                          </p>
                        </div>
                        <div v-if="job_meta.key === 'totalTime'">
                          <p>
                            Total Time:
                            {{
                              job_meta.value
                                | timeInFloatToSec
                                | timeInHoursMinutes
                            }}
                          </p>
                        </div>
                        <div v-if="job_meta.key === 'fee'">
                          <p>Fee: {{ job_meta.value | percentage }}</p>
                        </div>
                        <div v-if="job_meta.key === 'total'">
                          <h3>Total Price: {{ job_meta.value | currency }}</h3>
                        </div>
                      </div>
                    </b-col>
                  </b-row>
                </div>
              </div>
            </b-col>
          </b-row>
        </b-modal>
      </div>
    </b-container>
  </div>
</template>

<script>
let components = {}
if (process.browser) {
  const Calendar = require('~/components/Calendar').default
  components = {
    Calendar
  }
}
export default {
  components,
  head() {
    return {
      title:
        'Jobs | Compare low cost Man with a van quotes - book Man and van for Removals',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            'Jobs | Compare low cost Man with a van quotes - book Man and van for Removals'
        }
      ]
    }
  },
  data() {
    return {
      events: [],
      wallet: 0
    }
  },
  async mounted() {
    const response = await this.$axios
      .$get('/driver/jobs')
      .then(function(response) {
        // handle success
        return response
      })
      .catch()
    this.$store.dispatch('driver-jobs/setDriverJobs', response.data)

    if (Object.keys(this.driverJobsObject).length) {
      const eventObject = []
      for (const jobIndex in this.driverJobsObject) {
        for (const jobMetaIndex in this.driverJobsObject[jobIndex].job_metas) {
          if (
            this.driverJobsObject[jobIndex].job_metas[jobMetaIndex].key ===
            'movingDate'
          ) {
            eventObject.push({
              id: this.driverJobsObject[jobIndex].id,
              title: 'Job',
              date: this.driverJobsObject[jobIndex].job_metas[jobMetaIndex]
                .value
            })
          }
        }
      }
      this.events = eventObject
    }
  },
  methods: {}
}
</script>

<template>
  <div class="page-my-move">
    <h1 class="ui-title-page">My Move</h1>
    <div class="triagl triagl-btm"></div>
    <EmptySpace />
    <b-container>
      <b-alert show variant="primary">
        <h4 class="alert-heading mt-2">
          Your Man with a van quote could be as little as £50
        </h4>
      </b-alert>
      <form @submit.prevent="onSubmit">
        <b-row>
          <b-col>
            <!-- Van Size -->
            <div class="card mt-3 section_mod-2">
              <div class="card-body">
                <b-row>
                  <b-col lg>
                    <div class="ui-subtitle-block">CHOOSE VEHICLE SIZE</div>
                    <h2 class="ui-title-block">Which Vehicle Do You Need?</h2>
                    <div class="border-color border-color_default"></div>
                  </b-col>
                  <b-col lg>
                    <nuxt-link
                      to="size-calculator"
                      class="btn mb-1 btn-secondary btn-lg btn-block"
                      exact
                    >
                      Use Van Size Calculator
                    </nuxt-link>
                  </b-col>
                </b-row>
                <b-form-group class="text-center">
                  <b-form-radio-group
                    v-model="vanSizeComputed"
                    @input="setSerchMeta($event, 'vanSize')"
                    class="theme-green radio-van"
                    required
                  >
                    <b-row>
                      <b-col sm="6" md="3">
                        <b-form-radio value="1">
                          <img
                            v-if="vanSizeComputed === '1'"
                            src="~assets/images/vans/van-sm-alt.png"
                            alt="small van"
                            class="img-fluid radio-img"
                          />
                          <img
                            v-else
                            src="~assets/images/vans/van-sm.png"
                            alt="small van"
                            class="img-fluid radio-img"
                          />
                          Small Van
                        </b-form-radio>
                      </b-col>
                      <b-col sm="6" md="3">
                        <b-form-radio value="2">
                          <img
                            v-if="vanSizeComputed === '2'"
                            src="~assets/images/vans/van-md-alt.png"
                            alt="Medium van"
                            class="img-fluid radio-img"
                          />
                          <img
                            v-else
                            src="~assets/images/vans/van-md.png"
                            alt="Medium van"
                            class="img-fluid radio-img"
                          />
                          Medium Van
                        </b-form-radio>
                      </b-col>
                      <b-col sm="6" md="3">
                        <b-form-radio value="3">
                          <img
                            v-if="vanSizeComputed === '3'"
                            src="~assets/images/vans/van-lg-alt.png"
                            alt="Large van"
                            class="img-fluid radio-img"
                          />
                          <img
                            v-else
                            src="~assets/images/vans/van-lg.png"
                            alt="Large van"
                            class="img-fluid radio-img"
                          />
                          Large Van
                        </b-form-radio>
                      </b-col>
                      <b-col sm="6" md="3">
                        <b-form-radio value="4">
                          <img
                            v-if="vanSizeComputed === '4'"
                            src="~assets/images/vans/van-xl-alt.png"
                            alt="Giant van"
                            class="img-fluid radio-img"
                          />
                          <img
                            v-else
                            src="~assets/images/vans/van-xl.png"
                            alt="Giant van"
                            class="img-fluid radio-img"
                          />
                          Giant Van
                        </b-form-radio>
                      </b-col>
                    </b-row>
                  </b-form-radio-group>
                </b-form-group>
              </div>
            </div>

            <!-- Helpers Required -->
            <div class="card mt-3 section_mod-2 ">
              <div class="card-body">
                <div class="ui-subtitle-block">
                  CHOOSE THE NUMBER OF REQUIRED HELPER
                </div>
                <h2 class="ui-title-block">
                  Will You Need Help With Loading And Unloading?
                </h2>
                <div class="border-color border-color_default"></div>
                <b-form-group class="text-center">
                  <b-form-radio-group
                    v-model="helpersRequiredComputed"
                    @input="setSerchMeta($event, 'helpersRequired')"
                    class="theme-green radio-help"
                    required
                  >
                    <b-row>
                      <b-col sm="6" md="3">
                        <b-form-radio value="0">
                          <fa
                            v-if="helpersRequiredComputed === '0'"
                            :icon="['fas', 'user-slash']"
                            class="icon-dark"
                          />
                          <fa v-else :icon="['fas', 'user-slash']" />
                          No help needed
                        </b-form-radio>
                      </b-col>
                      <b-col sm="6" md="3">
                        <b-form-radio value="1">
                          <fa
                            v-if="helpersRequiredComputed === '1'"
                            :icon="['fas', 'user']"
                            class="icon-dark"
                          />
                          <fa v-else :icon="['fas', 'user']" />
                          Driver helping
                        </b-form-radio>
                      </b-col>
                      <b-col sm="6" md="3">
                        <b-form-radio value="2">
                          <fa
                            v-if="helpersRequiredComputed === '2'"
                            :icon="['fas', 'user-friends']"
                            class="icon-dark"
                          />
                          <fa v-else :icon="['fas', 'user-friends']" />
                          Driver helping + 1 helper
                        </b-form-radio>
                      </b-col>
                      <b-col sm="6" md="3">
                        <b-form-radio value="3">
                          <fa
                            v-if="helpersRequiredComputed === '3'"
                            :icon="['fas', 'users']"
                            class="icon-dark"
                          />
                          <fa v-else :icon="['fas', 'users']" />
                          Driver helping + 2 helpers
                        </b-form-radio>
                      </b-col>
                    </b-row>
                  </b-form-radio-group>
                </b-form-group>
              </div>
            </div>
            <b-alert show variant="primary" class="mt-3">
              <h4 class="alert-heading mt-2">
                Will I be able to travel in the Van to the destination?
              </h4>
              <p>
                Drivers at
                <nuxt-link to="/" exact>
                  Hellovans.com
                </nuxt-link>
                are happy to offer a seat in their vans to the destination,
                Number of seats available is based on the size of the van you
                require and the number of helpers you need, Its always best to
                check with the man and van provider once booked.
              </p>
            </b-alert>
            <!-- Date time -->
            <div class="card mt-3 section_mod-2">
              <div class="card-body">
                <div class="ui-subtitle-block">CHOOSE THE MOVING DATE</div>
                <h2 class="ui-title-block">When You're Moving?</h2>
                <div class="border-color border-color_default"></div>
                <datetime
                  v-model="movingDateComputed"
                  :value-zone="getUTCPlusTimeOffset"
                  @input="setSerchMeta($event, 'movingDate')"
                  @click.prevent="setChatWindowZIndex()"
                  class="theme-green"
                  type="datetime"
                  use12-hour
                  required
                ></datetime>
              </div>
            </div>

            <!-- description -->
            <div class="card mt-3 section_mod-2 ">
              <div class="card-body">
                <div class="ui-subtitle-block">
                  WRITE A NOTE FOR YOUR DRIVER
                </div>
                <h2 class="ui-title-block">Any Note?</h2>
                <div class="border-color border-color_default"></div>
                <b-form-group
                  label="Please enter a brief description of the items you will be moving and any additional contact numbers. Please also let us know if you need any items assembled or re-assembled."
                  label-for="description"
                >
                  <b-form-input
                    v-model="descriptionComputed"
                    @input="setSerchMeta($event, 'description')"
                  ></b-form-input>
                </b-form-group>
              </div>
            </div>

            <!-- Customer Info -->
            <div class="card mt-3 section_mod-2">
              <div class="card-body">
                <div class="ui-subtitle-block">
                  YOUR INFO
                  <span v-if="!authenticated">
                    ((We'll use this to create your account if you are not
                    logged in))
                  </span>
                  <span v-else></span>
                </div>
                <h2 class="ui-title-block">About You</h2>
                <div class="border-color border-color_default"></div>
                <b-row>
                  <b-col>
                    <b-form-group label="Name" label-for="customerInfoName">
                      <b-form-input
                        v-model="customerInfoNameComputed"
                        @input="setSerchMeta($event, 'customerInfoName')"
                        required
                      ></b-form-input>
                    </b-form-group>
                  </b-col>
                  <b-col>
                    <b-form-group label="Email" label-for="customerInfoEmail">
                      <b-form-input
                        v-model="customerInfoEmailComputed"
                        @input="setSerchMeta($event, 'customerInfoEmail')"
                        type="email"
                        required
                      ></b-form-input>
                    </b-form-group>
                  </b-col>
                  <b-col>
                    <b-form-group
                      label="Phone Number"
                      label-for="customerInfoPhone"
                    >
                      <b-form-input
                        v-model="customerInfoPhoneComputed"
                        @input="setSerchMeta($event, 'customerInfoPhone')"
                        required
                      ></b-form-input>
                    </b-form-group>
                  </b-col>
                </b-row>
              </div>
            </div>

            <!-- Where you're moving? -->
            <div class="card mt-3 section_mod-2 ">
              <div class="card-body">
                <div class="ui-subtitle-block">
                  COLLECTION, DELIVERY AND WAYPOINTS ADDRESSES
                </div>
                <h2 class="ui-title-block">Where You're Moving?</h2>
                <div class="border-color border-color_default"></div>
                <b-row>
                  <b-col md>
                    <b-row>
                      <b-col md>
                        <b-form-group>
                          Moving from address
                          <no-ssr>
                            <gmap-autocomplete
                              :value="collectionPlaceObject.address"
                              @place_changed="setCollectionPlace"
                              class="form-control"
                              placeholder="Collection Address"
                              required
                            ></gmap-autocomplete>
                          </no-ssr>
                        </b-form-group>
                      </b-col>
                      <b-col md>
                        <b-form-group>
                          At my collection address there
                          <b-form-select
                            :value="collectionPlaceObject.stairs"
                            :options="stairsOptions"
                            @input="setStairs($event, 'collection')"
                            required
                          ></b-form-select>
                        </b-form-group>
                      </b-col>
                    </b-row>

                    <b-row>
                      <b-col md>
                        <b-form-group>
                          Moving To address
                          <no-ssr>
                            <gmap-autocomplete
                              :value="deliveryPlaceObject.address"
                              @place_changed="setDeliveryPlace"
                              class="form-control"
                              placeholder="Delivery Address"
                              required
                            ></gmap-autocomplete>
                          </no-ssr>
                        </b-form-group>
                      </b-col>
                      <b-col md>
                        <b-form-group>
                          At my delivery address there
                          <b-form-select
                            :value="deliveryPlaceObject.stairs"
                            :options="stairsOptions"
                            @input="setStairs($event, 'delivery')"
                            required
                          ></b-form-select>
                        </b-form-group>
                      </b-col>
                    </b-row>

                    <b-button @click.prevent="addEmptyWayPoint" class="mb-3">
                      +
                      <fa :icon="['fas', 'map-marker-alt']" />
                      Add Stop
                    </b-button>
                    <div
                      v-for="(wayPointPlacesObjectSingle,
                      index) in wayPointPlacesObject"
                      :key="index"
                    >
                      <b-row>
                        <b-col md>
                          <div class="input-group mb-3">
                            <no-ssr>
                              <gmap-autocomplete
                                :value="wayPointPlacesObject[index].address"
                                @click="setCurrentWayPointIndex(index)"
                                @place_changed="setWayPointPlace"
                                class="form-control"
                                placeholder="Stop Address"
                                required
                              ></gmap-autocomplete>
                            </no-ssr>

                            <div
                              v-if="wayPointPlacesObject.length - 1 == index"
                              class="input-group-append"
                            >
                              <span
                                @click.prevent="deleteWayPoint(index)"
                                class="input-group-text bg-danger color-white"
                              >
                                X
                              </span>
                            </div>
                          </div>
                        </b-col>
                        <b-col md>
                          <b-form-group>
                            <b-form-select
                              :value="wayPointPlacesObject[index].stairs"
                              :options="stairsOptions"
                              @input="setStairs($event, 'waypoint', index)"
                              required
                            ></b-form-select>
                          </b-form-group>
                        </b-col>
                      </b-row>
                    </div>
                  </b-col>
                  <b-col md>
                    <b-button
                      v-if="
                        collectionPlaceObject.address &&
                          deliveryPlaceObject.address
                      "
                      @click="getDirection"
                      variant="primary"
                    >
                      <fa :icon="['fas', 'route']" />
                      Check Direction
                    </b-button>
                    <!-- Map -->
                    <no-ssr>
                      <gmap-map
                        ref="mapDir"
                        v-show="showMap"
                        :center="center"
                        :zoom="15"
                        class="mt-2"
                        style="width: 100%; height: 300px"
                      ></gmap-map>
                    </no-ssr>
                  </b-col>
                </b-row>
              </div>
            </div>

            <!-- Total Time -->
            <div class="card mt-3 section_mod-2">
              <div class="card-body">
                <div class="ui-subtitle-block">
                  NUMBER OF REQUIRED HOURS FOR THE THE MOVE TO BE COMPLETED
                </div>
                <h2 class="ui-title-block">
                  How Many Hours Do You Want The Vehicle For?
                </h2>
                <div class="border-color border-color_default"></div>
                <div class="row">
                  <div class="col-xs-12 col-sm-1">
                    <p>Estimated:</p>
                  </div>

                  <div class="col-xs-12 col-sm-3">
                    <p>
                      <fa :icon="['fas', 'road']" />
                      Travel time:
                      <strong>
                        <span id="estimated-driving-time">
                          {{ searchMetaObject.travelTime | timeInHoursMinutes }}
                        </span>
                      </strong>
                    </p>
                  </div>

                  <div class="col-xs-12 col-sm-5">
                    <p>
                      <fa :icon="['fas', 'truck-loading']" />
                      Loading and unloading time:
                      <strong>
                        <span id="estimated-loading-time">
                          {{
                            searchMetaObject.loadingUnloadingTime
                              | timeInHoursMinutes
                          }}
                        </span>
                      </strong>
                    </p>
                  </div>

                  <div class="col-xs-12 col-sm-3">
                    <p>
                      <fa :icon="['fas', 'clock']" />
                      We estimate you book:
                      <strong>
                        <span class="estimated-total-time">
                          {{
                            searchMetaObject.estimatedTotalTime
                              | timeInHoursMinutes
                          }}
                        </span>
                      </strong>
                    </p>
                  </div>
                </div>
                <b-form-group>
                  <b-form-select
                    v-model="totalTimeComputed"
                    :options="totalTimeOptions"
                    @input="setSerchMeta($event, 'totalTime')"
                    required
                  ></b-form-select>
                </b-form-group>
              </div>
            </div>

            <b-alert show variant="primary" class="mt-2">
              <p class="mt-3">
                We only charge you from the pick up to the delivery address, so
                <b>
                  you wont be charge for the time the van is on the way to the
                  pick up address.
                </b>
                Note: all drivers are pay as you go and you can extend it for as
                many hours as you like.
              </p>
            </b-alert>

            <!-- Notification -->
            <div class="card mt-3 section_mod-2 ">
              <div class="card-body">
                <div class="ui-subtitle-block">BY EMAIL AND SMS</div>
                <h2 class="ui-title-block">Notify Me</h2>
                <div class="border-color border-color_default"></div>
                <b-form-group
                  label="We'd love to keep in touch about this move by email and text message."
                >
                  <b-form-radio-group
                    v-model="notificationComputed"
                    :options="notificationOptions"
                    @input="setSerchMeta($event, 'notification')"
                    class="theme-green"
                    required
                  ></b-form-radio-group>
                </b-form-group>
              </div>
            </div>
          </b-col>
        </b-row>

        <b-row>
          <b-col md></b-col>
          <b-col md>
            <div class="card mt-3 section_mod-2 mb-3">
              <b-button block type="submit" size="lg">
                Get My Free Quotes
              </b-button>
            </div>
          </b-col>
          <b-col md></b-col>
        </b-row>
      </form>
    </b-container>
  </div>
</template>
<script>
import EmptySpace from '~/components/EmptySpace.vue'
/* global google */
export default {
  components: {
    EmptySpace
  },
  head() {
    return {
      title:
        'My Move | Compare low cost Man with a van quotes - book Man and van for Removals',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            'My Move | Compare low cost Man with a van quotes - book Man and van for Removals'
        }
      ]
    }
  },
  data() {
    return {
      vanSizeComputed: null,
      helpersRequiredComputed: null,
      movingDateComputed: null,
      descriptionComputed: ' ',
      customerInfoNameComputed: null,
      customerInfoEmailComputed: null,
      customerInfoPhoneComputed: null,
      totalTimeComputed: null,
      notificationComputed: null,
      vanSizeOptions: [
        { text: 'Small Van', value: '1' },
        { text: 'Medium Van', value: '2' },
        { text: 'Large Van', value: '3' },
        { text: 'Giant Van', value: '4' }
      ],
      helpersRequiredOptions: [
        { text: 'No help needed', value: '0' },
        { text: 'Driver helping', value: '1' },
        { text: 'Driver helping + 1 helper', value: '2' },
        { text: 'Driver helping + 2 helpers', value: '3' }
      ],
      collectionAddress: {
        stairs: null
      },
      deliveryAddress: {
        stairs: null
      },
      stairsOptions: [
        { text: 'At my address there', value: null },
        { text: 'are no flights of stairs', value: '0' },
        { text: 'is 1 flight of stairs', value: '1' },
        { text: 'are 2 flights of stairs', value: '2' },
        { text: 'are 3 flights of stairs', value: '3' },
        { text: 'are 4 flights of stairs', value: '4' },
        { text: 'are 5 flights of stairs', value: '5' },
        { text: 'are 6 flights of stairs', value: '6' },
        { text: 'are 7 flights of stairs', value: '7' },
        { text: 'are 8+ flights of stairs', value: '8' },
        { text: 'is a lift', value: '9' }
      ],
      totalTimeOptions: [
        /* { text: '30 minutes', value: '0.5' },
        { text: '1 hour', value: '1' },
        { text: '1 and a half hours', value: '1.5' }, */
        { text: '2 hour', value: '2' },
        { text: '2 and a half hours', value: '2.5' },
        { text: '3 hour', value: '3' },
        { text: '3 and a half hours', value: '3.5' },
        { text: '4 hour', value: '4' },
        { text: '4 and a half hours', value: '4.5' },
        { text: '5 hour', value: '5' },
        { text: '5 and a half hours', value: '4.5' },
        { text: '6 hour', value: '6' },
        { text: '6 and a half hours', value: '6.5' },
        { text: '7 hour', value: '7' },
        { text: '7 and a half hours', value: '7.5' },
        { text: '8 hour', value: '8' },
        { text: '8 and a half hours', value: '8.5' },
        { text: '9 hour', value: '9' },
        { text: '9 and a half hours', value: '9.5' },
        { text: '10 hour', value: '10' },
        { text: '10 and a half hours', value: '10.5' },
        { text: '11 hour', value: '11' },
        { text: '11 and a half hours', value: '11.5' },
        { text: '12 hour', value: '12' },
        { text: '12 and a half hours', value: '12.5' }
      ],
      notificationOptions: [
        { text: 'Yes', value: 'Yes' },
        { text: 'No', value: 'No' }
      ],
      // Map Data
      showMap: true,
      center: {
        lat: 51.507441,
        lng: -0.1277
      },

      currentWayPointIndex: 0,
      directionsService: null,
      directionsDisplay: null
    }
  },
  computed: {
    wayPoints() {
      const formatted = []
      let googleLatLng = {}
      for (let i = 0; i < this.wayPointPlacesObject.length; i++) {
        if (this.wayPointPlacesObject[i].address) {
          googleLatLng = new google.maps.LatLng(
            this.wayPointPlacesObject[i].lat,
            this.wayPointPlacesObject[i].lng
          )
          formatted[i] = {
            location: googleLatLng
          }
        }
      }
      return formatted
    },
    searchData() {
      return {
        collection: this.collectionPlaceObject,
        delivery: this.deliveryPlaceObject,
        waypoints: this.wayPointPlacesObject,
        vanSize: this.searchMetaObject.vanSize,
        movingDate: this.searchMetaObject.movingDate,
        helpersRequired: this.searchMetaObject.helpersRequired,
        description: this.searchMetaObject.description,
        customerInfoName: this.searchMetaObject.customerInfoName,
        customerInfoEmail: this.searchMetaObject.customerInfoEmail,
        customerInfoPhone: this.searchMetaObject.customerInfoPhone,
        notification: this.searchMetaObject.notification,
        loadingUnloadingTime: this.searchMetaObject.loadingUnloadingTime,
        travelTime: this.searchMetaObject.travelTime,
        totalTime: this.searchMetaObject.totalTime,
        milesDriven: this.searchMetaObject.milesDriven,
        stairsTime: this.searchMetaObject.stairsTime,
        estimatedTotalTime: this.searchMetaObject.estimatedTotalTime,
        weekDay: this.searchMetaObject.weekDay
      }
    },
    getUTCPlusTimeOffset() {
      const d = new Date()
      const n = d.getTimezoneOffset()
      let offset = ''
      if (n < 0) {
        offset = 'UTC+' + (-1 * n) / 60
      } else if (n < 0) {
        offset = 'UTC-' + n / 60
      } else {
        offset = 'UTC'
      }
      return offset
    }
  },
  mounted() {
    this.$nextTick(function() {
      this.$gmapApiPromiseLazy().then(() => {
        this.$options.directionsService = new google.maps.DirectionsService()
        this.$options.directionsDisplay = new google.maps.DirectionsRenderer()
        this.$options.directionsDisplay.setMap(this.$refs.mapDir.$mapObject)
      })
    })
    this.vanSizeComputed = this.searchMetaObject.vanSize
    this.helpersRequiredComputed = this.searchMetaObject.helpersRequired
    this.movingDateComputed = this.searchMetaObject.movingDate
    this.descriptionComputed = this.searchMetaObject.description
    this.customerInfoNameComputed = this.searchMetaObject.customerInfoName
    this.customerInfoEmailComputed = this.searchMetaObject.customerInfoEmail
    this.customerInfoPhoneComputed = this.searchMetaObject.customerInfoPhone
    this.totalTimeComputed = this.searchMetaObject.totalTime
    this.notificationComputed = this.searchMetaObject.notification
  },
  methods: {
    async setSerchMeta(event, value) {
      const metaObject = {
        [value]: event
      }
      await this.$store.dispatch('search/setSearchMetaValue', metaObject)
      if (value === 'movingDate') {
        const metaObjectWeekday = {
          weekDay: this.isoStringToDate(event).getDay()
        }
        await this.$store.dispatch(
          'search/setSearchMetaValue',
          metaObjectWeekday
        )
      }
    },
    async setStairs(event, locationType, index = null) {
      const placeArray = [event, locationType, index]
      await this.$store.dispatch('places/setStairsPlaces', placeArray)
      const metaObject = {
        stairsTime: this.getStairsTime()
      }
      await this.$store.dispatch('search/setSearchMetaValue', metaObject)
    },

    getStairsTime() {
      let collectionStairsTime = 0
      if (this.collectionPlaceObject.stairs < 9) {
        collectionStairsTime = this.collectionPlaceObject.stairs * 15
      } else {
        collectionStairsTime = 10
      }
      let deliveryStairsTime = 0
      if (this.deliveryPlaceObject.stairs < 9) {
        deliveryStairsTime = this.deliveryPlaceObject.stairs * 15
      } else {
        deliveryStairsTime = 10
      }
      let waypointStairsTime = 0
      if (this.wayPointPlacesObject.length >= 0) {
        for (let i = 0; this.wayPointPlacesObject.length > i; i++) {
          if (this.wayPointPlacesObject[i].stairs < 9) {
            waypointStairsTime =
              this.wayPointPlacesObject[i].stairs * 15 + waypointStairsTime
          } else {
            waypointStairsTime = 10 + waypointStairsTime
          }
        }
      }

      return (
        (collectionStairsTime + deliveryStairsTime + waypointStairsTime) * 60
      )
    },

    async onSubmit() {
      const responseData = await this.$axios
        .$post('/places', this.searchData)
        .then(function(response) {
          // handle success
          return response
        })
        .catch()
      await this.$axios
        .$post('/quotes', this.searchData)
        .then(function(response) {
          // handle success
          return response
        })
        .catch()
      await this.$store.dispatch('search-result/setSearchResult', responseData)
      this.$router.push('/my-quotes')
    },
    setChatWindowZIndex() {
      if (document.getElementById('tawkchat-container')) {
        document.getElementById('tawkchat-container').style.zIndex = 990
      }
    }
  }
}
</script>

<template>
  <div class="main-trust-box ">
    <b-container class="mt-5 mb-5">
      <b-row>
        <b-col class="text-center">
          <div
            v-html="landingHtmlObject.meta.trustBoxTitle"
            class="ui-title-block"
          ></div>
          <div class="border-color border-color_center"></div>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <no-ssr>
            <trustbox
              template-id="539ad60defb9600b94d7df2c"
              style-height="500px"
              style-width="100%"
              stars="3,4,5"
              theme="light"
              locale="en-GB"
            />
          </no-ssr>
          <!-- TrustBox widget - List -->
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

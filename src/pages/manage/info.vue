<template>
  <q-page padding class="constrain-page-width">
    <div v-if="getActiveGroupConfig" class="row q-col-gutter-md">

      <div class="col-xs-12">
        <q-card>
          <q-card-section>
            <img :src="getActiveGroupConfig.ui.logo"  style="width:100%; max-width:300px;">
          </q-card-section>
          <q-card-section>
            <q-item class="no-padding">
              <q-item-section>
                <q-item-label>Group Account</q-item-label>
                <q-item-label caption>{{getActiveGroupConfig.groupname}}</q-item-label>
              </q-item-section>
            </q-item>
            <div class="q-mt-md">About</div>
            <p class="text-grey-7 text-caption text-weight-light">{{getActiveGroupConfig.meta.about}}</p>

            <div class="text-weight-light row justify-between items-center">
            <div>
              <q-btn :disabled="!isValidUrl(getActiveGroupConfig.meta.url)" label="website" icon="link" color="primary" @click="openURL(getActiveGroupConfig.meta.url)">
                <q-tooltip content-class="bg-secondary">
                  {{getActiveGroupConfig.meta.url}}
                </q-tooltip>
              </q-btn>
            </div>
              <q-item>
                  <q-item-section >
                    <q-item-label caption>Created</q-item-label>
                    <q-item-label >{{getActiveGroupConfig.creation_date}}</q-item-label>

                  </q-item-section>
              </q-item>
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div class="col-xs-12 col-sm-6 col-lg-4">
        <q-card class="primary-hover-list">
          <q-item clickable :to="`/manage/${getActiveGroup}/custodians`">
            <q-item-section avatar>
              <q-icon name="mdi-account-key" color="primary" size="xl"/>
            </q-item-section>
            <q-item-section>
              <q-item-label class="text-weight-light text-h5 text-grey-7">Custodians</q-item-label>
            </q-item-section>
            <q-item-section side>
              <q-item-label class=" text-h5 text-grey-7">{{getNumberCustodians}}</q-item-label>
            </q-item-section>
          </q-item>
        </q-card>
      </div>

      <div v-if="getCoreConfig && getCoreConfig.conf.member_registration" class="col-xs-12 col-sm-6 col-lg-4">
        <q-card class="primary-hover-list">
          <q-item clickable >
            <q-item-section avatar>
              <q-icon name="mdi-account-multiple-check" color="primary" size="xl"/>
            </q-item-section>
            <q-item-section>
              <q-item-label class="text-weight-light text-h5 text-grey-7">Members</q-item-label>
            </q-item-section>
            <q-item-section side>
              <q-item-label v-if="getCoreState" class=" text-h5 text-grey-7">{{getCoreState.state.member_count}}</q-item-label>
            </q-item-section>
          </q-item>
        </q-card>
      </div>

      <div v-if="getCoreConfig && getCoreConfig.conf.maintainer_account" class="col-xs-12 col-sm-6 col-lg-4">
        <q-card class="primary-hover-list">
          <q-item clickable >
            <q-item-section avatar>
              <q-icon name="mdi-settings-transfer" color="primary" size="xl"/>
            </q-item-section>
            <q-item-section>
              <q-item-label class="text-weight-light text-h5 text-grey-7">Maintainer Account</q-item-label>
              <q-item-label caption >{{getCoreConfig.conf.maintainer_account}}</q-item-label>
            </q-item-section>
          </q-item>
        </q-card>
      </div>

    </div>
    <wasm-compiler :asbuffer="false"/>
    <!-- <pre>{{getActiveGroupConfig}}</pre> -->

  </q-page>
</template>

<script>
import { mapGetters } from "vuex";
import {openURL} from "quasar";
import {isValidUrl} from "../../imports/validators.js";

import wasmCompiler from "components/wasm-compiler";

export default {
  name: "PageIndex",
  components: {
    wasmCompiler
  },
  data() {
    return {

    };
  },
  computed: {
    ...mapGetters({
      getAccountName: "ual/getAccountName",
      getActiveGroup: "group/getActiveGroup",
      getActiveGroupConfig: "group/getActiveGroupConfig",
      getCoreConfig: "group/getCoreConfig",
      getCoreState: "group/getCoreState",
      getNumberCustodians: "group/getNumberCustodians"
    })
  },
  methods: {
    isValidUrl,
    openURL,
    dologin() {}
  }

};
</script>

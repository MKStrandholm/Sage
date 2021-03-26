<template>
  <div class="pb-5">
    <div
      class="container-fluid toolbar-shadow pb-3 pl-4"
      style="background-color: white; border-bottom: 2px solid #f1f1f1"
    >
      <div class="row p-1 align-items-center" style="height: 42px">
        <div class="col-sm-4">
          <h6 class="font-weight-bold mb-0 mt-0">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              fill="currentColor"
              class="bi bi-layout-sidebar-inset pr-1"
              style="padding-bottom: 3px"
              viewBox="0 0 16 16"
            >
              <path
                d="M8.186 1.113a.5.5 0 0 0-.372 0L1.846 3.5 8 5.961 14.154 3.5 8.186 1.113zM15 4.239l-6.5 2.6v7.922l6.5-2.6V4.24zM7.5 14.762V6.838L1 4.239v7.923l6.5 2.6zM7.443.184a1.5 1.5 0 0 1 1.114 0l7.129 2.852A.5.5 0 0 1 16 3.5v8.662a1 1 0 0 1-.629.928l-7.185 2.874a.5.5 0 0 1-.372 0L.63 13.09a1 1 0 0 1-.63-.928V3.5a.5.5 0 0 1 .314-.464L7.443.184z"
              />
            </svg>
            Assets
          </h6>
        </div>
        <div class="col"></div>
        <div class="col-4 text-right">
          <span
            @click="toggleAssetCard"
            class="icon-Info"
            :class="{ 'selected-item': this.$store.state.ui.assetCard }"
            style="
              font-size: 24px;
              padding-bottom: 0px;
              margin-right: -2px;
              vertical-align: middle;
              display: inline-block;
            "
          ></span>
        </div>
      </div>
      <hr class="mt-0" style="color: #f1f1f1" />
      <div class="">
        <div class="d-flex flex-wrap">
          <!-- Search input here -->
          <div class="bd-highlight w-50 input-group">
            <div class="input-group-prepend">
              <div class="input-group-text">
                <span
                  class="icon-MagnifyingGlass"
                  style="font-size: 20px; color: #000; vertical-align: middle"
                ></span>
              </div>
            </div>
            <!-- Search input here -->
            <input
              @change="changeType"
              v-on:keyup.enter="searchReset()"
              onclick="select()"
              v-model="searchParam"
              type="text"
              class="form-control bg-light"
              id="inlineFormInputGroupUsername2"
              placeholder="Search"
            />
            <div class="input-group-append">
              <button
                type="submit"
                class="btn btn-success"
                role="button"
                @click="searchReset()"
              >
                Search
              </button>
            </div>
          </div>
          <!-- ./ Search Input -->

          <div class="ml-auto bd-highlight">
            <button class="btn btn-light mr-2">
              <span
                class="icon-Sliders text-muted"
                style="
                  font-size: 18px;
                  font-weight: bold;
                  display: inline-block;
                "
              ></span>
            </button>
            <button
              type="button"
              class="btn btn-success badge-info"
              role="button"
            >
              Saved Searches
            </button>
          </div>
        </div>

        <!-- ./ Search Input -->
      </div>
    </div>

    <!-- Added for testing -->
    <!-- <div class="input-group mb-3">
        <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">@</span>
        </div>
        <input type="text" class="form-control w-25" placeholder="Username" aria-label="Username" aria-describedby="basic-addon1" v-model="searchParam">
    </div> -->
    <!-- Search Bar END-->

    <div class="row no-gutters assets-page-overflow">
      <!-- This is the Workspace/main content. Insert your page content in here, or else. -->
      <div class="col pt-3">
        <!-- Container-->

        <div class="container-fluid">
          <div class="row no-gutters pt-1 mb-1">
            <div class="col">
              <button @click="selectAll" class="btn font-weight-bold">
                Select All
                <svg
                  width="1.4em"
                  height="1.4em"
                  viewBox="0 0 16 16"
                  class="bi bi-check-all ml-1"
                  :class="{
                    'selected-item':
                      selectedAssets.length == searchResults.length,
                    'text-muted': selectedAssets.length != searchResults.length,
                  }"
                  style="border: 2px solid #f1f1f1; border-radius: 5px"
                  fill="currentColor"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M8.97 4.97a.75.75 0 0 1 1.071 1.05l-3.992 4.99a.75.75 0 0 1-1.08.02L2.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093L8.95 4.992a.252.252 0 0 1 .02-.022zm-.92 5.14l.92.92a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 1 0-1.091-1.028L9.477 9.417l-.485-.486-.943 1.179z"
                  />
                </svg>
              </button>

              <span v-if="selectedAssets.length == 0">
                <!-- # Results-->
                <!-- <span v-if="this.$store.state.assets.search != ''" class="ml-5 text-muted">
                                {{assetsSearched.length}} results for
                                <span class="text-success font-italic">
                                    {{this.$store.state.assets.search}}
                                    <span class="icon-MinusFilled" style="font-size: 18px; vertical-align: middle; "></span>
                                </span>
                                in Images.
                            </span> -->

                <!-- Consider... 
                            <span class="ml-3 text-muted">
                            Consider 
                            <span class="text-info font-italic">
                                Dodge of Venice 
                                <span class="icon-PlusFilled" style="font-size: 18px; vertical-align: middle; "></span>
                                ,
                            </span>
                            <span class="text-info font-italic">
                                Fransenco Molin 
                                <span class="icon-PlusFilled" style="font-size: 18px; vertical-align: middle; "></span>
                                ,
                            </span>
                            </span>
                            ./Consider... -->
              </span>
              <span v-else>
                <!-- Asset Selection -->
                <span class="text-info font-weight-bold">
                  {{ selectedAssets.length }} Selected
                </span>
                <span class="dropdown ml-2">
                  <button
                    class="btn btn-outline-dark dropdown-toggle"
                    style="padding-left: 1.75rem; padding-right: 1.75rem"
                    type="button"
                    id="dropdownMenuButton"
                    data-toggle="dropdown"
                    aria-haspopup="true"
                    aria-expanded="false"
                  >
                    Select Action
                  </button>
                  <div
                    class="dropdown-menu"
                    aria-labelledby="dropdownMenuButton"
                  >
                    <a
                      @click="openAddToFolderModal"
                      class="dropdown-item"
                      href="#"
                      >Add to Folder</a
                    >
                    <a
                      @click="openSaveToLightboxModal"
                      class="dropdown-item"
                      href="#"
                      >Save to Lightbox</a
                    >
                    <!-- <a @click="openShareMultipleModal" class="dropdown-item" href="#">Share</a>
                                    <a class="dropdown-item" href="#">Download</a>
                                    <a v-if="this.$store.state.assets.selectedAssets.length == 2" @click="openCompareAssetsModal" class="dropdown-item" href="#">Compare Assets</a>
                                    <a class="dropdown-item" href="#">Change Status</a>
                                    <a class="dropdown-item text-danger" href="#">Delete</a> -->
                  </div>
                </span>
                <button @click="clearSelection" class="btn">
                  Clear Selection
                </button>
              </span>
            </div>

            <div class="col-3">
              <!-- For spacing -->
            </div>

            <div class="col-2 text-right pr-2">
              <svg
                @click="view = 'thumbnail'"
                xmlns="http://www.w3.org/2000/svg"
                width="1.75rem"
                height="1.75rem"
                fill="currentColor"
                class="bi bi-grid mr-1 text-muted p-1"
                :class="{ 'text-info': view == 'thumbnail' }"
                viewBox="0 0 16 16"
              >
                <path
                  d="M1 2.5A1.5 1.5 0 0 1 2.5 1h3A1.5 1.5 0 0 1 7 2.5v3A1.5 1.5 0 0 1 5.5 7h-3A1.5 1.5 0 0 1 1 5.5v-3zM2.5 2a.5.5 0 0 0-.5.5v3a.5.5 0 0 0 .5.5h3a.5.5 0 0 0 .5-.5v-3a.5.5 0 0 0-.5-.5h-3zm6.5.5A1.5 1.5 0 0 1 10.5 1h3A1.5 1.5 0 0 1 15 2.5v3A1.5 1.5 0 0 1 13.5 7h-3A1.5 1.5 0 0 1 9 5.5v-3zm1.5-.5a.5.5 0 0 0-.5.5v3a.5.5 0 0 0 .5.5h3a.5.5 0 0 0 .5-.5v-3a.5.5 0 0 0-.5-.5h-3zM1 10.5A1.5 1.5 0 0 1 2.5 9h3A1.5 1.5 0 0 1 7 10.5v3A1.5 1.5 0 0 1 5.5 15h-3A1.5 1.5 0 0 1 1 13.5v-3zm1.5-.5a.5.5 0 0 0-.5.5v3a.5.5 0 0 0 .5.5h3a.5.5 0 0 0 .5-.5v-3a.5.5 0 0 0-.5-.5h-3zm6.5.5A1.5 1.5 0 0 1 10.5 9h3a1.5 1.5 0 0 1 1.5 1.5v3a1.5 1.5 0 0 1-1.5 1.5h-3A1.5 1.5 0 0 1 9 13.5v-3zm1.5-.5a.5.5 0 0 0-.5.5v3a.5.5 0 0 0 .5.5h3a.5.5 0 0 0 .5-.5v-3a.5.5 0 0 0-.5-.5h-3z"
                />
              </svg>

              <svg
                @click="view = 'list'"
                xmlns="http://www.w3.org/2000/svg"
                width="1.75rem"
                height="1.25rem"
                fill="currentColor"
                class="bi bi-list-ul mr-1 text-muted"
                :class="{ 'text-info': view == 'list' }"
                viewBox="0 0 16 16"
              >
                <path
                  fill-rule="evenodd"
                  d="M5 11.5a.5.5 0 0 1 .5-.5h9a.5.5 0 0 1 0 1h-9a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h9a.5.5 0 0 1 0 1h-9a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h9a.5.5 0 0 1 0 1h-9a.5.5 0 0 1-.5-.5zm-3 1a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm0 4a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm0 4a1 1 0 1 0 0-2 1 1 0 0 0 0 2z"
                />
              </svg>

              <svg
                @click="view = 'detail'"
                xmlns="http://www.w3.org/2000/svg"
                width="1.75rem"
                height="1.25rem"
                fill="currentColor"
                class="bi bi-distribute-vertical mr-1 text-muted"
                :class="{ 'text-info ': view == 'detail' }"
                viewBox="0 0 16 16"
              >
                <path
                  fill-rule="evenodd"
                  d="M1 1.5a.5.5 0 0 0 .5.5h13a.5.5 0 0 0 0-1h-13a.5.5 0 0 0-.5.5zm0 13a.5.5 0 0 0 .5.5h13a.5.5 0 0 0 0-1h-13a.5.5 0 0 0-.5.5z"
                />
                <path
                  d="M2 7a1 1 0 0 1 1-1h10a1 1 0 0 1 1 1v2a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V7z"
                />
              </svg>
            </div>
            <div></div>
          </div>

          <!-- Asset Thumbnail View-->
          <div
            v-if="view == 'thumbnail'"
            :class="{
              'asset-container-padding': !this.$store.state.ui.assetCard,
            }"
            ref="example"
          >
            <div class="asset-container container-fluid">
              <h6 class="text-center font-italic" v-if="!searchResults.length">
                Search had no matches...
              </h6>

              <div
                class="asset-item m-2"
                v-for="(asset, index) in searchResults"
                :key="index"
              >
                <AssetThumbnail
                  @directDownload="directDownload(asset.id)"
                  @assetSelected="assetSelected"
                  @passData="pipeData($event)"
                  :asset="asset"
                  :selected="selectedAssets.includes(asset.id)"
                  @openDoka="openDokaModal(asset.id, asset.title)"
                  class="h-100"
                />
              </div>
            </div>
          </div>

          <!-- Asset Detail View -->
          <div v-if="view == 'detail'">
            <h6 class="text-center font-italic" v-if="!searchResults.length">
              Search had no matches...
            </h6>
            <ul class="pl-0 asset-container">
              <li
                class="asset-item m-2"
                v-for="(asset, index) in searchResults"
                :key="index"
              >
                <AssetDetail
                  :asset="asset"
                  :selected="selectedAssets.includes(asset.id)"
                  class="h-100"
                />
              </li>
            </ul>
          </div>

          <!-- Asset List View -->
          <div v-if="view == 'list'" class="container-fluid mt-4">
            <table class="table table-hover table-sm">
              <h6 class="text-center font-italic" v-if="!searchResults.length">
                Search had no matches...
              </h6>
              <thead v-else>
                <tr>
                  <th style="border-top: none"></th>
                  <th style="border-top: none" class="w-50">Title</th>
                  <th style="border-top: none">File Type</th>
                  <th style="border-top: none">File Dimensions</th>
                  <th style="border-top: none">File Size</th>
                </tr>
              </thead>

              <tbody>
                <tr
                  v-for="(asset, index) in searchResults"
                  :key="index"
                  :class="{ 'text-info': isSelected(asset.id) }"
                >
                  <th scope="row">
                    <input
                      :checked="isSelected(asset.id)"
                      @click="selectAsset(asset.id)"
                      type="checkbox"
                      aria-label="Checkbox for following text input"
                    />
                  </th>
                  <td @click="setSelectedAssetId(asset.id)">
                    <img
                      style="max-width: 24px; max-height: 24px"
                      class="mr-2"
                      :src="asset.thumbnail_url"
                      alt=""
                    />
                    {{ asset.title }}
                  </td>
                  <td>{{ asset.type }}</td>
                  <td>680 x 420 px</td>
                  <td>{{ asset.size }}</td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- ./Container -->
        </div>
        <infinite-loading
          class="p-3"
          spinner="spiral"
          :identifier="infiniteId"
          @infinite="infiniteHandler"
        >
          <span class="p-3" slot="no-more">- No more results -</span>
        </infinite-loading>
        <!-- ./Workspace-->
      </div>
    </div>

    <!-- ./Container -->

    <!-- ./Workspace-->

    <!-- <CompareAssetsModal /> -->
    <!-- <ShareMultipleModal /> -->
    <!-- <ShareModal /> -->
    <SaveToLightboxModal
      ref="SaveToLightboxModal"
      :selectedAssets="selectedAssets"
    />
    <AddToFolderModal ref="AddToFolderModal" :selectedAssets="selectedAssets" />

    <!-- <div v-if="dokaAsset != null"> -->
    <!-- <DokaModal v-if="('blob' in asset) && dokaOpened"  utils="crop,filter,color,markup,resize" :crop-aspect-ratio-options="cropOptions" :src="asset.blob" @confirm="handleDokaConfirm" @cancel="handleDokaCancel" @close="enabled=false" /> -->
    <DokaModal
      v-if="dokaOpened"
      utils="crop,filter,color,markup,resize"
      :crop-aspect-ratio-options="cropOptions"
      :src="dokaUrl"
      @confirm="handleDokaConfirm"
      @cancel="handleDokaCancel"
      @close="enabled = false"
    />
    <!-- </div> -->
  </div>
</template>

<script>
import AssetThumbnail from "@/components/ui/AssetThumbnail";
import AssetDetail from "@/components/ui/AssetDetail";
import Pagination from "@/components/ui/Pagination";
import ShareModal from "@/components/modals/ShareModal";
import ShareMultipleModal from "@/components/modals/ShareMultipleModal";
import SaveToLightboxModal from "@/components/modals/SaveToLightboxModal";
import AddToFolderModal from "@/components/modals/AddToFolderModal";
import CompareAssetsModal from "@/components/modals/CompareAssetsModal";
import ToolbarDetailsModeButton from "@/components/ui/details-mode/ToolbarDetailsModeButton";
import feathersClient from "@/config/feathers-client.js";
const simpleSearchService = feathersClient.service("simple-search");
const directDownloadService = feathersClient.service("direct-download");
const debounce = require("lodash.debounce");
// const assetService = feathersClient.service('assets');
import { DokaModal, toURL } from "@/components/vue-doka/";

export default {
  name: "Assets",
  layout: "defaultAssetCard",
  components: {
    AssetThumbnail,
    AssetDetail,
    Pagination,
    ShareModal,
    ShareMultipleModal,
    SaveToLightboxModal,
    AddToFolderModal,
    CompareAssetsModal,
    DokaModal,
    toURL,
  },
  data() {
    return {
      dokaAsset: null,
      selectedAssets: [],
      pagesMin: 1,
      pagesMax: 0,
      currentPage: 1,
      per: 25,
      pageNumber: 0,
      searchResults: [],
      searchParam: "",
      view: "thumbnail",
      dokaOpened: false,
      cropOptions: [
        {
          label: "Free",
          value: null,
        },
        {
          label: "Portrait",
          value: 1.5,
        },
        {
          label: "Square",
          value: 1,
        },
        {
          label: "Landscape",
          value: 0.75,
        },
      ],
      filter: "Date",
      dokaUrl: "",
      dokaAssetTitle: "",
      infiniteId: +new Date(),
    };
  },
  computed: {
    updateSelectAll: {
      get: function () {
        return this.selectAll;
      },
      set: function () {
        let self = this;
        this.selectAll = !this.selectAll;
        this.searchResults.forEach((result) => {
          profile.selected = !profile.selected;
          console.log(profile);
        });
      },
    },
    assets: function () {
      if (this.filter == "Date") {
        return this.$store.state.assets.assets
          .filter((a) => a.title.match(this.searchReg))
          .slice(this.page * this.per, this.page * this.per + this.per);
      } else if (this.filter == "Name") {
        return this.$store.state.assets.assets
          .filter((a) => a.title.match(this.searchReg))
          .sort((a, b) => (a.title > b.title ? 1 : -1))
          .slice(this.page * this.per, this.page * this.per + this.per);
      }
    },
  },
  watch: {
    "$route.query.q"() {
      this.searchRouterLink();
      this.searchReset();
    },
  },
  methods: {
    /**
     * When a user clicks on the checkbox of an asset thumbnail "assetSelected" is emited from the component
     * This function is then called.
     * All this function does is push this asset into the selectedAssets[] or remove it if the asset is already in the array
     *
     *      - Patrick Malara Feb 18th
     */

    assetSelected(assetId) {
      let index = this.selectedAssets.findIndex((a) => a == assetId);
      if (index == -1) {
        this.selectedAssets.push(assetId);
      } else {
        this.selectedAssets.splice(index, 1);
      }
      console.log(this.selectedAssets);
    },

    setSelectedAssetId(assetId) {
      this.$store.dispatch("assets/setSelectedAssetId", assetId);

      if (!this.$store.state.ui.assetCard) {
        this.$store.commit("ui/toggleAssetCard");
      }
    },
    selectAsset(assetId) {
      this.$store.dispatch("assets/selectAsset", assetId);
    },
    isSelected: function (assetId) {
      var index = this.$store.state.assets.selectedAssets.findIndex(
        (id) => id == assetId
      );
      return index == -1 ? false : true;
    },
    selectAll() {
      this.selectedAssets = [];
      this.searchResults.forEach((asset) => {
        this.selectedAssets.push(asset.id);
      });
      //this.$store.dispatch('assets/selectAll');
    },
    clearSelection() {
      this.selectedAssets = [];
      //this.$store.dispatch('assets/clearSelection');
    },

    openSaveToLightboxModal() {
      this.$refs.SaveToLightboxModal.show();
      //this.$modal.show('SaveToLightboxModal');
    },

    openAddToFolderModal() {
      this.$refs.AddToFolderModal.show();
      //this.$modal.show('AddToFolderModal');
    },

    openCompareAssetsModal() {
      this.$modal.show("CompareAssetsModal");
    },

    openShareMultipleModal() {
      this.$modal.show("ShareMultipleModal");
    },

    toggleAssetCard: function () {
      if (this.$store.state.lightbox.lightboxCard) {
        this.$store.commit("lightbox/toggleLightboxCard");
      }
      this.$store.commit("ui/toggleAssetCard");
    },

    directDownload(asset_id) {
      directDownloadService.get(asset_id).then((res) => {
        console.log(res);

        const url = res;
        const a = document.createElement("a");

        a.href = url;
        a.download = asset_id || "download";

        const clickHandler = () => {
          setTimeout(() => {
            URL.revokeObjectURL(url);
            window.removeEventListener("click", clickHandler);
          }, 150);
        };

        a.addEventListener("click", clickHandler, false);

        a.click();
      });
    },

    /* Doka Modal Functions*/
    handleDokaConfirm(output) {
      console.log("Confirm crop!", output);
      this.dokaOpened = false;

      // Create an object URL for the blob object
      const url = URL.createObjectURL(output.file);

      const a = document.createElement("a");

      a.href = url;
      a.download = this.dokaAssetTitle || "download";

      const clickHandler = () => {
        setTimeout(() => {
          URL.revokeObjectURL(url);
          window.removeEventListener("click", clickHandler);
        }, 150);
      };

      a.addEventListener("click", clickHandler, false);

      a.click();
    },
    handleDokaCancel() {
      console.log("Cancel crop!");
      this.dokaOpened = false;
    },
    openDokaModal(asset_id, asset_title) {
      directDownloadService.get(asset_id).then((res) => {
        console.log(res);
        this.dokaUrl = res;
        this.dokaOpened = true;
        this.dokaAssetTitle = asset_title;
      });
    },
    /*  -Simple Search + Infinity Scroll-
            @author: Allan L
            :Infinite scroll runs without mounted, the infiniteHandler() will automatically ping the DB so dont woryy about it.

                    *searchQuery() - Returns the query object.

                    *infiniteQuery() - Will run the query and concatenate the response into list and return the response length.

                    *infiniteHandler() - Will run infiniteQuery, will load more assets until the total count of responses in the query have been hit.

                    *searchReset()- A click event for the search bar that will empty the list set the route, and run infiniteQuery based off search params.

                    *pageCounter() - Get total results and find the inate page count from that.

                    *increment() - Does what you think it will.

                    *searchRouterLink() - Will change ths search param to the route query if it exists, if not it will leave it empty.

                    *changeType() - Will reset the infinite scroll plugin, each time a search happens.
        */
    searchQuery(self) {
      return {
        query: {
          search: self.searchParam,
          limit: self.per,
          pagination: self.currentPage,
        },
      };
    },
    async infiniteQuery() {
      let self = this;
      let resLength = 0;
      let queryResponse = (res) => {
        let assets = res["assets"];
        if (!assets[0]) {
          resLength = 0;
        } else if (self.searchResults.length < assets[0].full_count) {
          this.pageCounter(assets[0].full_count, self);
          this.increment();
          resLength = assets.length;
          self.searchResults.push(...assets);
        }
        return resLength;
      };
      const result = await simpleSearchService
        .find(this.searchQuery(self))
        .then(queryResponse);
      return result;
    },
    async infiniteHandler($state) {
      const newAssetCount = await this.infiniteQuery();
      return newAssetCount > 0 ? $state.loaded() : $state.complete();
    },
    searchReset() {
      let self = this;
      let queryRoute = "/assets/?q=";
      this.$router.push(queryRoute + this.searchParam);
      self.searchResults = [];
      self.currentPage = 1;
      this.infiniteQuery();
    },
    pageCounter: function (resultCount, self) {
      self.pagesMax = Math.ceil(resultCount / self.per);
    },
    increment: function () {
      this.currentPage =
        this.currentPage === this.pagesMax
          ? this.pagesMax
          : this.currentPage + 1;
    },
    searchRouterLink() {
      this.searchParam =
        this.$route.query.q === undefined ? "" : this.$route.query.q;
    },
    changeType() {
      this.infiniteId += 1;
    },
    // This method receives the position/assetID data from the EditThumbnailPositionModal in order to re-render the image after a successful thumbnail change
    pipeData($event) {
      // Find all of the card items on the assets page that are being rendered
      let cards = document.getElementsByClassName("card-img-top");
      // Iterate through each card, checking if the src of the card img matches the src passed in by the event that was emitted
      for (let card of cards) {
        if (card.src === $event.src) {
          // Match has been found
          //console.log(card);
          // Update the style of the card to match the newly set value
          card.style = $event.thumbnailPosition;
        }
      }
    }
  },
  mounted() {
    this.searchRouterLink();
    if (!this.$store.state.ui.search) {
      this.$store.commit("ui/toggleComponent", "search");
    }
    this.$store.dispatch("assets/setSearch", "");
  },
};
</script>

<style>
.asset-container {
  display: grid;
  grid-gap: 0.6em;
  grid-template-columns: repeat(5, minmax(8rem, 1fr));
  grid-auto-rows: minmax(256px, auto);
}

.assets-page-overflow {
  height: calc(100vh - 160px);
  overflow-y: scroll;
}

.current-page {
  text-decoration: underline;
}

.skip-page {
  color: #a51890;
  border: 1px solid #a51890;
  padding: 8px 14px;
}

.current {
  color: rgb(81, 14, 168);
}

ul {
  padding: 0;
  list-style-type: none;
}

li {
  display: inline;
}

a.first::after {
  content: "...";
}

a.last::before {
  content: "...";
}
</style>
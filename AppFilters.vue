<template>
  <div  class="filters-nav-container" v-if="typeFilters === 'type-01'">
    <div class="filters-nav-wrapper">
      <div class="d-flex justify-content-center filters-nav-top">
        <div class="d-inline-flex">
          <button
            type="button"
            class="d-inline-flex align-items-center justify-content-center filter-btn"
            :class="searchType == 'Buy' ? 'active' : ''"
            @click="searchType = 'Buy'"
          >
            Comprar
          </button>
          <button
            type="button"
            class="d-inline-flex align-items-center justify-content-center filter-btn"
            :class="searchType == 'Rent' ? 'active' : ''"
            @click="searchType = 'Rent'"
          >
            Arrendar
          </button>
          <button
            type="button"
            class="d-inline-flex align-items-center justify-content-center filter-btn"
            :class="searchType == 'Trespass' ? 'active' : ''"
            @click="searchType = 'Trespass'"
          >
            Trespasse
          </button>
        </div>
      </div>
      <div
        class="d-flex flex-column flex-md-row align-items-center filters-nav-bottom"
      >
        <div class="left">
          <!--INSTEAD OF DIV CAN BE A FORM... -->
          <div>
            <div
              class="d-flex flex-column flex-md-row align-items-center form-row"
            >
              <div class="col-12 col-md-5 col-lg-4">
                <div class="form-group m-0 p-0">
                  <!--<div
                    class="custom-select big normal"
                    :class="{ active: fieldHouse, open: selectHouseOpen }"
                    @click="selectHouseOpen = !selectHouseOpen"
                  >
                    SELECT OPTION
                    <div class="selected" v-if="!fieldHouse">Tipo Imóvel</div>
                    <div class="selected" v-else>{{ fieldHouse }}</div>
                    <div class="items">
                      <div @click="fieldHouse = ' Imóvel 01'">
                        <span> Imóvel 01</span>
                      </div>
                      <div @click="fieldHouse = ' Imóvel 02'">
                        <span> Imóvel 02</span>
                      </div>
                      <div @click="fieldHouse = ' Imóvel 03'">
                        <span> Imóvel 03 </span>
                      </div>
                    </div>
                  </div>-->
                  <Multiselect
                    v-model="propertyType"
                    placeholder="Tipo de Imóvel"
                    :options="['Imóvel1', 'Imóvel2', 'Imóvel3']"
                  />
                </div>
              </div>
              <div class="col-12 col-md-7 col-lg-8">
                <div class="form-group m-0 p-0">
                  <div class="d-flex align-items-center">
                    <span
                      class="d-inline-flex align-items-center justify-content-center icon"
                      ><LazySvgLocation
                    /></span>
                    <div class="field-input big">
                      <input
                        type="text"
                        placeholder="Procure por localização"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="right">
          <div
            class="d-flex align-items-center justify-content-between justify-content-md-end"
          >
            <button
              type="button"
              class="d-inline-flex d-lg-none align-items-center justify-content-center filters-btn mobile"
              @click="handleFiltersMobile"
            >
              <LazySvgFilters />
            </button>
            <button
              type="button"
              class="d-none d-lg-inline-flex align-items-center justify-content-center filters-btn desktop"
              @click="handleFiltersDesktop"
            >
              <LazySvgFilters />
            </button>
            <button
              type="submit"
              class="d-none d-md-inline-flex d-lg-none align-items-center justify-content-center filters-btn-search"
            >
              <LazySvgSearch />
            </button>
            <button
              type="submit"
              class="d-inline-flex d-md-none d-lg-inline-flex align-items-center justify-content-center custom-btn big rose-background"
            >
              <span>Pesquisar</span>
            </button>
          </div>
        </div>
      </div>
      <transition name="slide-fade">
      <div
        class="filters-nav-full-optiopns-wrapper homepage"
        v-if="toggleFiltersDesktop"
      >
        <div class="filters-nav-full-top">
          <div
            class="d-flex flex-column flex-md-row align-items-center form-row"
          >
            <div class="col-3">
              <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Nome do Empreendimento</label>
                  <input v-model="fieldName" type="text" placeholder="Nome do empreendimento" />
                </div>
              </div>
            </div>
            <div class="col-3">
              <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Referência Imóvel</label>
                  <input v-model="fieldReference" type="text" placeholder="Referência imóvel" />
                </div>
              </div>
            </div>
            <div class="col-3">
              <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Estado da Construção</label>
                  <div
                    class="custom-select big normal"
                    :class="{ active: fieldState, open: selectStateOpen }"
                    @click="selectToggle('fieldstate')"
                  >
                    <!--SELECT OPTION-->
                    <div class="selected" v-if="!fieldState">Selecione</div>
                    <div class="selected" v-else>{{ fieldState }}</div>
                    <div class="items">
                      <div @click="fieldState = 'Novo'">
                        <span> Novo</span>
                      </div>
                      <div @click="fieldState = 'Semi-Novo'">
                        <span> Semi-Novo</span>
                      </div>
                      <div @click="fieldState = 'Usado'">
                        <span> Usado </span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-3">
              <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">As Nossas Lojas</label>
                  <div
                    class="custom-select big normal"
                    :class="{ active: fieldStores, open: selectStoresOpen }"
                    @click="selectToggle('fieldstores')"
                  >
                    <!--SELECT OPTION-->
                    <div class="selected" v-if="!fieldStores">Selecione</div>
                    <div class="selected" v-else>{{ fieldStores }}</div>
                    <div class="items">
                      <div @click="fieldStores = 'Store 01'">
                        <span> Store 01</span>
                      </div>
                      <div @click="fieldStores = 'Store 02'">
                        <span> Store 02</span>
                      </div>
                      <div @click="fieldStores = 'Store 03'">
                        <span> Store 03 </span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="filters-nav-full-bottom">
          <div
            class="d-flex flex-column flex-md-row align-items-center form-row"
          >
          <div class="col-3">
            <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Tipologia</label>          
                  <div
                  class="custom-select big normal"
                  :class="{ active: fieldTypology, open: selectTypologyOpen }"
                  @click="selectToggle('fieldtypology')"
                >
                  <!--SELECT OPTION-->
                  <div class="selected" v-if="!fieldTypology">Selecione</div>
                    <div class="selected" v-else>{{ fieldTypology }}</div>
                    <div class="items">
                      <div @click="fieldTypology = 'T1'">
                        <span> T1</span>
                      </div>
                      <div @click="fieldTypology = 'T2'">
                        <span> T2</span>
                      </div>
                      <div @click="fieldTypology = 'T3'">
                        <span> T3 </span>
                      </div>
                    </div>
                  </div>
                </div>
            </div>
          </div>
          <div class="col-3">
            <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Quartos</label>          
                  <div
                  class="custom-select big normal"
                  :class="{ active: fieldBedrooms, open: selectBedroomsOpen }"
                  @click="selectToggle('fieldbedrooms')"
                >
                  <!--SELECT OPTION-->
                  <div class="selected" v-if="!fieldBedrooms">Selecione</div>
                    <div class="selected" v-else>{{ fieldBedrooms }}</div>
                    <div class="items">
                      <div @click="fieldBedrooms = '1'">
                        <span> 1</span>
                      </div>
                      <div @click="fieldBedrooms = '2'">
                        <span> 2</span>
                      </div>
                      <div @click="fieldBedrooms = '3'">
                        <span> 3 </span>
                      </div>
                    </div>
                  </div>
                </div>
            </div>
          </div>
          <div class="col-3">
            <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Preço</label>          
                  <div
                  class="custom-select big normal"
                  :class="{ active: fieldPrice, open: selectPriceOpen }"
                  @click="selectToggle('fieldprice')"
                >
                  <!--SELECT OPTION-->
                  <div class="selected" v-if="!fieldPrice">Selecione</div>
                    <div class="selected" v-else>{{ fieldPrice }}</div>
                    <div class="items">
                      <div @click="fieldPrice = '100'">
                        <span> 100</span>
                      </div>
                      <div @click="fieldPrice = '200'">
                        <span> 200</span>
                      </div>
                      <div @click="fieldPrice = '300'">
                        <span> 300</span>
                      </div>
                    </div>
                  </div>
                </div>
            </div>
          </div>
          <div class="col-3">
            <div class="form-group m-0 p-0">
                <div class="field-input filters">
                  <label class="filter-title">Área Útil</label>          
                  <div
                  class="custom-select big normal"
                  :class="{ active: fieldMeters, open: selectMetersOpen }"
                  @click="selectToggle('fieldmeters')"
                >
                  <!--SELECT OPTION-->
                  <div class="selected" v-if="!fieldMeters">Selecione</div>
                    <div class="selected" v-else>{{ fieldMeters }}</div>
                    <div class="items">
                      <div @click="fieldMeters = '100'">
                        <span> 100</span>
                      </div>
                      <div @click="fieldMeters = '200'">
                        <span> 200</span>
                      </div>
                      <div @click="fieldMeters = '300'">
                        <span> 300 </span>
                      </div>
                    </div>
                  </div>
                </div>
            </div>
          </div>

          </div>
        </div>
        <div class="filters-nav-full-bottom">
          <div
            class="d-flex flex-column flex-md-row align-items-center form-row"
          >
            <div class="col-5">
              <div class="form-group m-0 p-0">
                <label class="filter-title">Estado</label>
                <div
                  class="d-flex align-items-center justify-content-start flex-wrap filters-wrapper"
                >
                  <div class="checkbox-wrapper filters">
                    <label for="Novo" class="d-inline-flex align-items-center">
                      <input v-model="fieldCheckedCondition" type="checkbox" id="Novo" value="New" />
                      <p>Novo</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label for="Usado" class="d-inline-flex align-items-center">
                      <input v-model="fieldCheckedCondition" type="checkbox" id="Usado" value="Used" />
                      <p>Usado</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Renovado"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedCondition" type="checkbox" id="Renovado" value="Renovated" />
                      <p>Renovado</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Construção"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedCondition" type="checkbox" id="Construção" value="Construction" />
                      <p>Construção</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Planta"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedCondition" type="checkbox" id="Planta" value="Plan" />
                      <p>Planta</p>
                    </label>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-7">
              <div class="form-group m-0 p-0">
                <label class="filter-title">Outras Características</label>
                <div
                  class="d-flex align-items-center justify-content-start flex-wrap filters-wrapper"
                >
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Jardim"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Jardim" value="Garden" />
                      <p>Jardim</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Piscina"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Piscina" value="Pool" />
                      <p>Piscina</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Varanda"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Varanda" value="Balcony" />
                      <p>Varanda</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Terraço"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Terraço" value="Terrace" />
                      <p>Terraço</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label for="Vista" class="d-inline-flex align-items-center">
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Vista" value="View" />
                      <p>Vista</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Elevador"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Elevador" value="Elevator" />
                      <p>Elevador</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Arrecadação"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Arrecadação" value="Storage" />
                      <p>Arrecadação</p>
                    </label>
                  </div>
                  <div class="checkbox-wrapper filters">
                    <label
                      for="Garagem"
                      class="d-inline-flex align-items-center"
                    >
                      <input v-model="fieldCheckedQualities" type="checkbox" id="Garagem" value="Garage" />
                      <p>Garagem</p>
                    </label>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="filters-nav-full-bottom btn d-flex justify-content-end">
          <button
            type="button"
            class="clear-filters-btn"
            @click="resetSelect"
          >
            <span>Limpar Filtros</span>
          </button>
        </div>
        <div class="filters-nav-full-bottom d-flex justify-content-end">
        <button
            type="button"
            class="d-none d-xl-inline-flex justify-content-between align-items-center justify-content-center filters-btn-products"
            @click="handleFiltersDesktop"
          >
            <LazySvgFilters />
            <span>Menos Filtros</span>
          </button>
        </div>
      </div>
      </transition>
    </div>
  </div>
  <div
    class="filters-nav-products-container"
    v-else-if="typeFilters === 'type-02'"
  >
    <div class="d-flex align-items-center filters-nav-products-wrapper">
      <div class="left">
        <div class="d-none d-xl-inline-flex field-input filters">
          <div
            class="custom-select small border-radius"
            :class="{ active: fieldPurpose, open: selectPurposeOpen }"
            @click="selectToggle('fieldpurpose')"
          >
            <!--SELECT OPTION-->
            <div v-if="!fieldPurpose">
              <div class="selected">Propósito</div>
              <div class="items">
                <div v-for="(value, index) in purposes" :key="index" @click="fieldPurpose = value">
                  <span> {{value}} </span>
                </div>
                <!-- <div @click="fieldPurpose = 'Comprar'">
                  <span> Comprar </span>
                </div>
                <div @click="fieldPurpose = 'Arrendar'">
                  <span> Arrendar </span>
                </div>
                <div @click="fieldPurpose = 'Trespasse'">
                  <span> Trespasse </span>
                </div> -->
              </div>
            </div>
            <div v-else>
              <div class="selected" @click="fieldPurpose = ''">
                {{ fieldPurpose }}
              </div>
            </div>
          </div>
        </div>
        <div class="d-none d-xl-inline-flex field-input filters">
          <div
            class="custom-select small border-radius"
            :class="{ active: fieldTypology, open: selectTypologyOpen }"
            @click="selectToggle('fieldtypology')"
          >
            <!--SELECT OPTION-->
            <div v-if="!fieldTypology">
              <div class="selected">Tipologia</div>
              <div class="items">
                <div @click="fieldTypology = 'T1'">
                  <span> T1</span>
                </div>
                <div @click="fieldTypology = 'T2'">
                  <span> T2</span>
                </div>
                <div @click="fieldTypology = 'T3'">
                  <span> T3 </span>
                </div>
              </div>
            </div>
            <div v-else>
              <!--OPTION CLICK AND REMOVE-->
              <div class="selected" @click="fieldTypology = ''">
                {{ fieldTypology }}
              </div>
            </div>
          </div>
        </div>
        <div class="d-none d-xl-inline-flex field-input filters">
          <div
            class="custom-select small border-radius"
            :class="{ active: fieldBedrooms, open: selectBedroomsOpen }"
            @click="selectToggle('fieldbedrooms')"
          >
            <!--SELECT OPTION-->
            <div v-if="!fieldBedrooms">
              <div class="selected">Quartos</div>
              <div class="items">
                <div @click="fieldBedrooms = '1'">
                  <span> 1</span>
                </div>
                <div @click="fieldBedrooms = '2'">
                  <span> 2</span>
                </div>
                <div @click="fieldBedrooms = '3'">
                  <span> 3 </span>
                </div>
              </div>
            </div>
            <div v-else>
              <!--OPTION CLICK AND REMOVE-->
              <div class="selected" @click="fieldBedrooms = ''">
                {{ fieldBedrooms }}
              </div>
            </div>
          </div>
        </div>
        <div class="d-none d-xl-inline-flex field-input filters">
          <div
            class="custom-select small border-radius"
            :class="{ active: fieldPrice, open: selectPriceOpen }"
            @click="selectToggle('fieldprice')"
          >
            <!--SELECT OPTION-->
            <div v-if="!fieldPrice">
              <div class="selected">Preço</div>
              <div class="items">
                <div @click="fieldPrice = '100'">
                  <span> 100</span>
                </div>
                <div @click="fieldPrice = '200'">
                  <span> 200</span>
                </div>
                <div @click="fieldPrice = '300'">
                  <span> 300 </span>
                </div>
              </div>
            </div>
            <div v-else>
              <!--OPTION CLICK AND REMOVE-->
              <div class="selected" @click="fieldPrice = ''">
                {{ fieldPrice }}
              </div>
            </div>
          </div>
        </div>
        <div class="d-none d-xl-inline-flex field-input filters">
          <div
            class="custom-select small border-radius"
            :class="{ active: fieldMeters, open: selectMetersOpen }"
            @click="selectToggle('fieldmeters')"
          >
            <!--SELECT OPTION-->
            <div v-if="!fieldMeters">
              <div class="selected">Área Útil</div>
              <div class="items">
                <div @click="fieldMeters = '100'">
                  <span> 100</span>
                </div>
                <div @click="fieldMeters = '200'">
                  <span> 200</span>
                </div>
                <div @click="fieldMeters = '300'">
                  <span> 300 </span>
                </div>
              </div>
            </div>
            <div v-else>
              <!--OPTION CLICK AND REMOVE-->
              <div class="selected" @click="fieldMeters = ''">
                {{ fieldMeters }}
              </div>
            </div>
          </div>
        </div>
        <div class="d-inline-flex">
          <button
            type="button"
            class="d-inline-flex d-xl-none justify-content-center align-items-center justify-content-center filters-btn-products"
            @click="handleFiltersMobile"
          >
            <LazySvgFilters />
            <span class="d-none d-md-block">+ Filtros</span>
          </button>
          <button
            type="button"
            class="d-none d-xl-inline-flex justify-content-between align-items-center justify-content-center filters-btn-products"
            @click="handleFiltersDesktop"
          >
            <LazySvgFilters />
            <span>+ Filtros</span>
          </button>
          <button
            type="button"
            class="d-none d-xl-inline-flex align-items-center justify-content-center clear-filters-btn"
            @click="resetSelect"
          >
            <span>Limpar Filtros</span>
          </button>
        </div>
      </div>
      <div class="right">
        <div class="d-flex flex-wrap align-items-center justify-content-end">
          <div
            class="d-inline-flex align-items-center switch-order-wrapper"
            v-if="sortProduct"
          >
            <p>Ordenar por:</p>
            <!--ADD CLASS 'down' TO CHANGE THE DIRECTION OF SVG-->
            <button
              type="button"
              class="d-inline-flex align-items-center order-btn down"
            >
              Popular
              <SvgArrowUp />
            </button>
          </div>
          <div class="d-inline-flex align-items-center switch-list-wrapper">
            <label class="switch-list">
              <input type="checkbox" class="switch" />
              <span class="slider" @click="handleTypeList"></span>
            </label>
            <p>Mapa</p>
          </div>
        </div>
      </div>
    </div>
    <transition name="slide-fade">
    <div
      class="filters-nav-full-optiopns-wrapper"
      v-if="toggleFiltersDesktop"
    >
      <div class="filters-nav-full-top">
        <div class="d-flex flex-column flex-md-row align-items-center form-row">
          <div class="col-3">
            <div class="form-group m-0 p-0">
              <div class="field-input filters">
                <label class="filter-title">Nome do Empreendimento</label>
                <input v-model="fieldName" type="text" placeholder="Insira aqui o nome do empreendimento" />
              </div>
            </div>
          </div>
          <div class="col-3">
            <div class="form-group m-0 p-0">
              <div class="field-input filters">
                <label class="filter-title">Referência Imóvel</label>
                <input v-model="fieldReference" type="text" placeholder="Insira aqui o nome do imóvel" />
              </div>
            </div>
          </div>
          <div class="col-3">
            <div class="form-group m-0 p-0">
              <div class="field-input filters">
                <label class="filter-title">Estado da Construção</label>
                <div
                  class="custom-select big normal"
                  :class="{ active: fieldState, open: selectStateOpen }"
                  @click="selectToggle('fieldstate')"
                >
                  <!--SELECT OPTION-->
                  <div class="selected" v-if="!fieldState">Selecione</div>
                  <div class="selected" v-else>{{ fieldState }}</div>
                  <div class="items">
                    <div @click="fieldState = 'Novo'">
                      <span> Novo</span>
                    </div>
                    <div @click="fieldState = 'Semi-Novo'">
                      <span> Semi-Novo</span>
                    </div>
                    <div @click="fieldState = 'Usado'">
                      <span> Usado </span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-3">
            <div class="form-group m-0 p-0">
              <div class="field-input filters">
                <label class="filter-title">As Nossas Lojas</label>
                <div
                  class="custom-select big normal"
                  :class="{ active: fieldStores, open: selectStoresOpen }"
                  @click="selectToggle('fieldstores')"
                >
                  <!--SELECT OPTION-->
                  <div class="selected" v-if="!fieldStores">Selecione</div>
                  <div class="selected" v-else>{{ fieldStores }}</div>
                  <div class="items">
                    <div @click="fieldStores = 'Store 01'">
                      <span> Store 01</span>
                    </div>
                    <div @click="fieldStores = 'Store 02'">
                      <span> Store 02</span>
                    </div>
                    <div @click="fieldStores = 'Store 03'">
                      <span> Store 03 </span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="filters-nav-full-bottom">
        <div class="d-flex flex-column flex-md-row align-items-center form-row">
          <div class="col-5">
            <div class="form-group m-0 p-0">
              <label class="filter-title">Estado</label>
              <div
                class="d-flex align-items-center justify-content-start flex-wrap filters-wrapper"
              >
                <div class="checkbox-wrapper filters">
                  <label for="Novo" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedCondition" type="checkbox" id="Novo" value="New"/>
                    <p>Novo</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Usado" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedCondition" type="checkbox" id="Usado" value="Used" />
                    <p>Usado</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label
                    for="Renovado"
                    class="d-inline-flex align-items-center"
                  >
                    <input v-model="fieldCheckedCondition" type="checkbox" id="Renovado" value="Renovated" />
                    <p>Renovado</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label
                    for="Construção"
                    class="d-inline-flex align-items-center"
                  >
                    <input v-model="fieldCheckedCondition" type="checkbox" id="Construção" value="Construction" />
                    <p>Construção</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Planta" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedCondition" type="checkbox" id="Planta" value="Plan" />
                    <p>Planta</p>
                  </label>
                </div>
              </div>
            </div>
          </div>
          <div class="col-7">
            <div class="form-group m-0 p-0">
              <label class="filter-title">Outras Características</label>
              <div
                class="d-flex align-items-center justify-content-start flex-wrap filters-wrapper"
              >
                <div class="checkbox-wrapper filters">
                  <label for="Jardim" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Jardim" value="Garden" />
                    <p>Jardim</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Piscina" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Piscina" value="Pool" />
                    <p>Piscina</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Varanda" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Varanda" value="Balcony" />
                    <p>Varanda</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Terraço" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Terraço" value="Terrace" />
                    <p>Terraço</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Vista" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Vista" value="View" />
                    <p>Vista</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label
                    for="Elevador"
                    class="d-inline-flex align-items-center"
                  >
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Elevador" value="Elevator" />
                    <p>Elevador</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label
                    for="Arrecadação"
                    class="d-inline-flex align-items-center"
                  >
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Arrecadação" value="Storage" />
                    <p>Arrecadação</p>
                  </label>
                </div>
                <div class="checkbox-wrapper filters">
                  <label for="Garagem" class="d-inline-flex align-items-center">
                    <input v-model="fieldCheckedQualities" type="checkbox" id="Garagem" value="Garage" />
                    <p>Garagem</p>
                  </label>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    </transition>
  </div>
</template>
<script setup>

import { defineComponent } from "vue";
import Multiselect from '@vueform/multiselect'
import { useFilterStore } from '@/store/filters'
import { storeToRefs } from "pinia";

const components = defineComponent({
  Multiselect,
});
 
const searchType = ref("Buy");
const fieldName = ref("");
const fieldReference = ref("");
const fieldCheckedCondition = ref([]);
const fieldCheckedQualities = ref([]);
const toggleFiltersDesktop = ref(false);
const selectPurposeOpen = ref(false);
const selectTypologyOpen = ref(false);
const selectHouseOpen = ref(false);
const selectBedroomsOpen = ref(false);
const selectPriceOpen = ref(false);
const selectMetersOpen = ref(false);
const selectStateOpen = ref(false);
const selectStoresOpen = ref(false);
const fieldPurpose = ref("");
const fieldTypology = ref("");
const fieldHouse = ref("");
const fieldBedrooms = ref("");
const fieldPrice = ref("");
const fieldMeters = ref("");
const fieldState = ref("");
const fieldStores = ref("");
const sortProduct = ref(true);
const emit = defineEmits(["toggleFiltersSidebar"]);
const props = defineProps({
  typeFilters: {
    type: String,
  },
});

const selectToggle = (elm) => {
  if (elm === 'fieldprice') {
    selectPriceOpen.value = !selectPriceOpen.value;
    selectPurposeOpen.value = false;
    selectTypologyOpen.value = false;
    selectBedroomsOpen.value = false;
    selectMetersOpen.value = false;
    selectStateOpen.value = false;
    selectStoresOpen.value = false;
  }
   if (elm === 'fieldstate') {
    selectStateOpen.value = !selectStateOpen.value;
    selectPurposeOpen.value = false;
    selectTypologyOpen.value = false;
    selectBedroomsOpen.value = false;
    selectMetersOpen.value = false;
    selectPriceOpen.value = false;
    selectStoresOpen.value = false;
  } 
  if (elm === 'fieldpurpose') {
    selectPurposeOpen.value = !selectPurposeOpen.value;
    selectStateOpen.value = false;
    selectTypologyOpen.value = false;
    selectBedroomsOpen.value = false;
    selectMetersOpen.value = false;
    selectPriceOpen.value = false;
    selectStoresOpen.value = false;
  } 
  if (elm === 'fieldtypology') {
    selectTypologyOpen.value = !selectTypologyOpen.value;
    selectPurposeOpen.value = false;
    selectStateOpen.value = false;
    selectBedroomsOpen.value = false;
    selectMetersOpen.value = false;
    selectPriceOpen.value = false;
    selectStoresOpen.value = false;
  } 
  if (elm === 'fieldbedrooms') {
    selectBedroomsOpen.value = !selectBedroomsOpen.value;
    selectPurposeOpen.value = false;
    selectStateOpen.value = false;
    selectTypologyOpen.value = false;
    selectMetersOpen.value = false;
    selectPriceOpen.value = false;
    selectStoresOpen.value = false;
  } 
  if (elm === 'fieldmeters') {
    selectMetersOpen.value = !selectMetersOpen.value;
    selectPurposeOpen.value = false;
    selectStateOpen.value = false;
    selectTypologyOpen.value = false;
    selectBedroomsOpen.value = false;
    selectPriceOpen.value = false;
    selectStoresOpen.value = false;
  } 
  if (elm === 'fieldstores') {
    selectStoresOpen.value = !selectStoresOpen.value;
    selectPurposeOpen.value = false;
    selectStateOpen.value = false;
    selectTypologyOpen.value = false;
    selectBedroomsOpen.value = false;
    selectPriceOpen.value = false;
    selectMetersOpen.value = false;
  } 
}

const resetSelect = () => {

fieldPurpose.value = "";
fieldBedrooms.value = "";
fieldPrice.value = "";
fieldTypology.value = "";
fieldMeters.value = "";
fieldState.value = "";
fieldStores.value = "";
fieldName.value = "";
fieldReference.value = "";
fieldCheckedCondition.value = [];
fieldCheckedQualities.value = [];

};

const handleFiltersDesktop = () => {
  toggleFiltersDesktop.value = !toggleFiltersDesktop.value;
};
const handleFiltersMobile = () => {
  emit("toggleFiltersSidebar");
};
const handleTypeList = () => {
  sortProduct.value = !sortProduct.value;
  emit("toggleTypeList");
};

const closeCustomSelectOutside = () => {
  let elm = document.getElementsByTagName("body");
  let elmSelect = document.querySelectorAll(".custom-select .selected");
  if (elm && elmSelect) {
    elm[0].addEventListener("click", (event) => {
      if (
        !(elmSelect[0] == event.target || elmSelect[0].contains(event.target))
      ) {
        selectHouseOpen
          ? (selectHouseOpen.value = false)
          : (selectHouseOpen.value = true);
      }
    });
  }
};

const closeCustomSelectInside = () => {
  let elm01 = document.querySelector(".filters-nav-full-optiopns-wrapper");
  let elmSelect = document.querySelectorAll(".custom-select .selected");
  if (elm01 && elmSelect) {
    elm01.addEventListener("click", (event) => {
      if (elm01 == event.target) {
        selectStateOpen
          ? (selectStateOpen.value = false)
          : (selectStateOpen.value = true);
        selectStoresOpen
          ? (selectStoresOpen.value = false)
          : (selectStoresOpen.value = true);
      }
    });
  }
};



const filterStore = useFilterStore();
const { locations, purposes, rooms, types } = storeToRefs(filterStore);

onMounted(() => {
  // store.fetchFilters()
  closeCustomSelectOutside();
  closeCustomSelectInside();
});


</script>
<style src="@vueform/multiselect/themes/default.css"></style>


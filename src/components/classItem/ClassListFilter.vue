<template>
    <div>
        <h4 class="mb-1 text-gray-700">ច្រោះទិន្នន័យ៖</h4>
        <div class="row">
            <div class="col-sm-6 col-md-6 col-xl-3">
                <!-- User Input Fields for Filtering -->
                <input class="form-control my-2 py-2" v-model="tempFilters.schoolName" @keydown.enter="applyFilter"
                    placeholder="អង្គភាព" />
            </div>

            <div class="col-sm-6 col-md-6 col-xl-3">
                <!-- <input class="form-control" v-model="tempFilters.province" @keydown.enter="applyFilter"
                    placeholder="រាជធានី ខេត្ត" /> -->
                <!-- <input class="form-control" v-model="tempFilters.type" @keydown.enter="applyFilter" placeholder="ប្រភេទសាលា" /> -->
                <select class="form-select my-2 py-2" v-model="tempFilters.province" aria-label="Select example">
                    <option value="">-- រាជធានី ខេត្ត --</option>
                    <option v-for="province in provinceData" :value="province">{{ province }}</option>
                </select>
            </div>

            <div class="col-sm-6 col-md-6 col-xl-3">
                <!-- <input class="form-control" v-model="tempFilters.type" @keydown.enter="applyFilter" placeholder="ប្រភេទសាលា" /> -->
                <select class="form-select my-2 py-2" v-model="tempFilters.type" aria-label="Select example">
                    <option value="">-- ប្រភេទសាលា --</option>
                    <option v-for="type in schoolTypes" :value="type">{{ type }}</option>
                </select>
            </div>

            <div class="col-sm-6 col-md-6 col-xl-3 d-flex justify-content-between align-items-center">
                <!-- Checkbox for Model School Standard Status -->
                <div class="form-check form-check-custom form-check-sm my-2 py-2">
                    <input class="form-check-input" type="checkbox" value="" id="flexCheckChecked"
                        v-model="tempFilters.modelSchoolStandardStatus" @keydown.enter="applyFilter" />
                    <label class="form-check-label" for="flexCheckChecked">
                        ជាប់ស្ដង់ដា
                    </label>
                </div>
                <!-- 
        <label>
            <input type="checkbox" v-model="tempFilters.modelSchoolStandardStatus" @keydown.enter="applyFilter" />
            ជាប់ស្ដង់ដា
        </label> -->
                <!-- Filter Button -->
                <button class="btn btn-sm btn-primary" @click="applyFilter">ស្វែងរក</button>

            </div>
        </div>
    </div>

    <div class="row d-flex justify-content-center">
        <div class="col-md-12 border-top my-5 mw-300px">

        </div>
    </div>

    <!-- Filtered Results -->
    <div class="card mt-5">
        <div class="card-body">
            <div class="d-flex align-items-top justify-content-between">
                <div style="width: 100%;">
                    <!--begin::Accordion-->
                    <div class="accordion accordion-icon-toggle" id="kt_accordion_1">
                        <!--begin::Item-->
                        <div class="mb-0">
                            <!--begin::Header-->
                            <div class="accordion-header py-2 d-flex collapsed" data-bs-toggle="collapse"
                                data-bs-target="#kt_accordion_1_item_1">
                                <span class="accordion-icon">
                                    <!--begin::Svg Icon | path: icons/duotone/Navigation/Right-2.svg-->
                                    <span class="svg-icon svg-icon-6">
                                        <svg xmlns="http://www.w3.org/2000/svg"
                                            xmlns:xlink="http://www.w3.org/1999/xlink" width="24px" height="24px"
                                            viewBox="0 0 24 24" version="1.1">
                                            <g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                                                <polygon points="0 0 24 0 24 24 0 24" />
                                                <rect fill="#000000" opacity="0.5"
                                                    transform="translate(8.500000, 12.000000) rotate(-90.000000) translate(-8.500000, -12.000000)"
                                                    x="7.5" y="7.5" width="2" height="9" rx="1" />
                                                <path
                                                    d="M9.70710318,15.7071045 C9.31657888,16.0976288 8.68341391,16.0976288 8.29288961,15.7071045 C7.90236532,15.3165802 7.90236532,14.6834152 8.29288961,14.2928909 L14.2928896,8.29289093 C14.6714686,7.914312 15.281055,7.90106637 15.675721,8.26284357 L21.675721,13.7628436 C22.08284,14.136036 22.1103429,14.7686034 21.7371505,15.1757223 C21.3639581,15.5828413 20.7313908,15.6103443 20.3242718,15.2371519 L15.0300721,10.3841355 L9.70710318,15.7071045 Z"
                                                    fill="#000000" fill-rule="nonzero"
                                                    transform="translate(14.999999, 11.999997) scale(1, -1) rotate(90.000000) translate(-14.999999, -11.999997)" />
                                            </g>
                                        </svg>
                                    </span>
                                    <!--end::Svg Icon-->
                                </span>
                                <h6 class="fs-7 text-gray-800 fw-bold mb-0 ms-1">
                                    <span class="">បង្ហាញ</span>៖ {{ filteredData.length }}/{{ schoolData.length }}
                                </h6>
                            </div>
                            <!--end::Header-->
                            <!--begin::Body-->
                            <div id="kt_accordion_1_item_1" class="collapse fs-6 ps-7" data-bs-parent="#kt_accordion_1">
                                <div class="">
                                    - {{ SRS }}៖ <b>{{ countSchoolType(SRS) }}</b>
                                </div>
                                <div class="">
                                    - {{ NWS }}៖ <b>{{ countSchoolType(NWS) }}</b>
                                </div>
                                <div class="">
                                    - {{ GSE }}៖ <b>{{ countSchoolType(GSE) }}</b>
                                </div>
                                <div class="">
                                    - {{ TechnicalSchool }}៖ <b>{{ countSchoolType(TechnicalSchool) }}</b>
                                </div>
                                <div class="pb-5">

                                </div>
                            </div>
                            <!--end::Body-->
                        </div>
                        <!--end::Item-->

                    </div>
                    <!--end::Accordion-->

                    <div class="accordion accordion-icon-toggle" id="kt_accordion_2">
                        <!--begin::Item-->
                        <div class="mb-5">
                            <!--begin::Header-->
                            <div class="accordion-header py-2 d-flex collapsed" data-bs-toggle="collapse"
                                data-bs-target="#kt_accordion_1_item_2">
                                <span class="accordion-icon">
                                    <!--begin::Svg Icon | path: icons/duotone/Navigation/Right-2.svg-->
                                    <span class="svg-icon svg-icon-6">
                                        <svg xmlns="http://www.w3.org/2000/svg"
                                            xmlns:xlink="http://www.w3.org/1999/xlink" width="24px" height="24px"
                                            viewBox="0 0 24 24" version="1.1">
                                            <g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                                                <polygon points="0 0 24 0 24 24 0 24" />
                                                <rect fill="#000000" opacity="0.5"
                                                    transform="translate(8.500000, 12.000000) rotate(-90.000000) translate(-8.500000, -12.000000)"
                                                    x="7.5" y="7.5" width="2" height="9" rx="1" />
                                                <path
                                                    d="M9.70710318,15.7071045 C9.31657888,16.0976288 8.68341391,16.0976288 8.29288961,15.7071045 C7.90236532,15.3165802 7.90236532,14.6834152 8.29288961,14.2928909 L14.2928896,8.29289093 C14.6714686,7.914312 15.281055,7.90106637 15.675721,8.26284357 L21.675721,13.7628436 C22.08284,14.136036 22.1103429,14.7686034 21.7371505,15.1757223 C21.3639581,15.5828413 20.7313908,15.6103443 20.3242718,15.2371519 L15.0300721,10.3841355 L9.70710318,15.7071045 Z"
                                                    fill="#000000" fill-rule="nonzero"
                                                    transform="translate(14.999999, 11.999997) scale(1, -1) rotate(90.000000) translate(-14.999999, -11.999997)" />
                                            </g>
                                        </svg>
                                    </span>
                                    <!--end::Svg Icon-->
                                </span>
                                <h6 class="fs-7 text-gray-800 fw-bold mb-0 ms-1">
                                    {{ filters.type[0] != '' && filters.type.length > 0 ? `${filters.type[0]} ` :
                                        'សាលា' }}ដែលនៅក្នុងខេត្តចំនួន
                                    {{ provinceList.length }} <b>{{
                                        }}</b>
                                </h6>
                            </div>
                            <!--end::Header-->
                            <!--begin::Body-->
                            <div id="kt_accordion_1_item_2" class="collapse fs-6 ps-7" data-bs-parent="#kt_accordion_2">

                                <div>
                                    <FilterByProvince :provinceList="provinceList"></FilterByProvince>
                                </div>
                            </div>
                            <!--end::Body-->
                        </div>
                        <!--end::Item-->
                    </div>
                </div>

                <div class="dropdown" style="position: absolute; right: 20px;">
                    <button class="btn bg-light-warning fs-7 py-1 px-2 text-nowrap" type="button"
                        data-bs-toggle="dropdown" aria-expanded="false">
                        បញ្ជីសាលា
                    </button>
                    <ul class="dropdown-menu">
                        <li><a target="_blank"
                                class="dropdown-item btn btn-xs btn-light py-2 text-gray-800 border-bottom"
                                style="border-radius: 0%;"
                                href="https://drive.google.com/file/d/1DinD0TA2Xu32_p2lA9YhgdGSCFktGqXI/view?usp=sharing">PDF</a>
                        </li>
                        <li><a target="_blank" class="dropdown-item btn btn-xs btn-light py-2 text-gray-800 border-top"
                                style="border-radius: 0%;"
                                href="https://api.codemie.dev/file/259-stepup-schools-excel">Excel (Zip)</a>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="table-responsive">
                <table class="table table-striped text-nowrap">
                    <thead>
                        <tr class="fs-6 text-gray-800 border-bottom-2 border-gray-200">
                            <th>ល.រ</th>
                            <th class="" style="font-weight: 600;">រាជធានី ខេត្ត</th>
                            <th class="" style="font-weight: 600;">អង្គភាព</th>
                            <th class="" style="font-weight: 600;">ប្រភេទសាលា</th>
                            <th class="min-w-100px" style="font-weight: 600;">ព្រឹត្តិបត្រព័ត៌មាន</th>
                            <th class="min-w-100px" style="font-weight: 600;">របាយការណ៍អធិការកិច្ច</th>
                            <th class="min-w-100px" style="font-weight: 600;">ស្វ័យវាយតម្លៃ</th>
                            <th class="min-w-100px" style="font-weight: 600;">ពិន្ទុ</th>
                            <th class="min-w-100px" style="font-weight: 600;">ក្រុមការងារវាយតម្លៃ</th>
                            <th class="min-w-100px" style="font-weight: 600;">ពិន្ទុ</th>
                            <th class="min-w-50px" style="font-weight: 600;">ជាប់ស្ដង់ដាសាលាមធ្យមសិក្សាគំរូ ឆ្នាំ2024
                            </th>
                            <th class="min-w-100px" style="font-weight: 600;">សាលាប្រើប្រាស់ MIS</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(item, index) in filteredData" :key="item.id">
                            <td>{{ item.id }}</td>
                            <td>{{ item.province }}</td>
                            <td>{{ item.schoolName }}</td>
                            <td><span v-for="(t, i) in item.type" style="">{{ t.replace(i > 0 ? SRS : '-', '-')
                                    }}</span>
                            </td>
                            <td><a v-if="item.profileLink != ''" :href="item.profileLink" target="_blank">ទាញយកទីនេះ</a>
                            </td>
                            <td><a v-if="item.inspectionReportLink != ''" :href="item.inspectionReportLink"
                                    target="_blank">ទាញយកទីនេះ</a></td>
                            <td><a v-if="item.selfEvalLink != ''" :href="item.selfEvalLink"
                                    target="_blank">ទាញយកទីនេះ</a></td>
                            <td>{{ item.selfEvalScore }}</td>
                            <td><a v-if="item.workingGroupEvalLink != ''" :href="item.workingGroupEvalLink"
                                    target="_blank">ទាញយកទីនេះ</a></td>
                            <td>{{ item.workingGroupEvalScore }}</td>
                            <td>
                                <!-- {{ item.modelSchoolStandardStatus ? 'ជាប់' : 'មិនជាប់' }} -->
                            </td>
                            <td>{{ item.useSchoolMgmtSystem }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>

        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import schoolData from '@/data/schoolData';
import provinceData from '@/data/provinceData';
import { GSE, NWS, SRS, SRSChinaAid, TechnicalSchool, schoolTypes } from '@/data/schoolType';
import FilterByProvince from './FilterByProvince.vue';

// Sample data
const dataList = ref(schoolData);

// Temporary filters that the user types before applying the filter
const tempFilters = ref({
    schoolName: '',
    province: '',
    type: '',
    modelSchoolStandardStatus: false // Unchecked by default
});

// Active filters for actual filtering after button click or Enter key press
const filters = ref({
    schoolName: '',
    province: '',
    type: [],
    modelSchoolStandardStatus: false
});

// Function to apply the temporary filter values to the actual filters on button click or Enter key press
const applyFilter = () => {
    //filters.value = { ...tempFilters.value };
    filters.value.schoolName = tempFilters.value.schoolName;
    filters.value.province = tempFilters.value.province;
    filters.value.type = [tempFilters.value.type]; // Copy the array
    filters.value.modelSchoolStandardStatus = tempFilters.value.modelSchoolStandardStatus;
};

// Computed property to filter data based on the filters
const filteredData = computed(() => {
    return dataList.value.filter(item => {
        return (
            // Check schoolName filter
            (!filters.value.schoolName || item.schoolName.toLowerCase().includes(filters.value.schoolName.toLowerCase())) &&

            // Check province filter
            (!filters.value.province || item.province.toLowerCase().includes(filters.value.province.toLowerCase())) &&

            // Check type filter (if there are selected types)
            (filters.value.type.length === 0 || filters.value.type.some(filterType =>
                item.type.some(type => type.toLowerCase().includes(filterType.toLowerCase()))
            )) &&

            // Check modelSchoolStandardStatus filter
            (!filters.value.modelSchoolStandardStatus || item.modelSchoolStandardStatus === filters.value.modelSchoolStandardStatus)
        );
    });
});

const countSchoolType = (schoolType) => {
    return filteredData.value.filter(item =>
        item.type.some(type => type.toLowerCase().includes(schoolType.toLowerCase()))
    ).length;
};

const provinceList = computed(() => {
    /*
    {
        "Phnom Penh": 2,
        "Siem Reap": 2,
        "Battambang": 1
    }
    */
    const countsByProvince = filteredData.value.reduce((acc, item) => {
        const key = item.province;
        if (!acc[key]) {
            acc[key] = 0;  // Initialize the count if it doesn't exist
        }
        acc[key] += 1;  // Increment the count
        return acc;
    }, {});

    var sortedProvinceByCount = Object.entries(countsByProvince)
        // Sort by count in descending order
        .sort(([, countA], [, countB]) => countB - countA);
    /*
    [
        { "name": "Phnom Penh", "count": 2 },
        { "name": "Siem Reap", "count": 2 },
        { "name": "Battambang", "count": 1 }
    ]
    */
    return sortedProvinceByCount.map(([name, count]) => ({
        name,
        count
    }));

});

// // Group by 'province'
// const groupedByProvince = data.reduce((acc, item) => {
//   const key = item.province;
//   if (!acc[key]) {
//     acc[key] = [];  // Create an array if it doesn't exist
//   }
//   acc[key].push(item);  // Push the item into the correct group
//   return acc;
// }, {});

// console.log(groupedByProvince);
/*
{
  "Phnom Penh": [
    { "id": 1, "province": "Phnom Penh", "name": "School A" },
    { "id": 3, "province": "Phnom Penh", "name": "School C" }
  ],
  "Siem Reap": [
    { "id": 2, "province": "Siem Reap", "name": "School B" },
    { "id": 5, "province": "Siem Reap", "name": "School E" }
  ],
  "Battambang": [
    { "id": 4, "province": "Battambang", "name": "School D" }
  ]
}

*/

// const provinceList2 = () => {
//     return filteredData.value.map((item) => item.province);
// }
</script>
<template>
    <div>
        <h4 class="mb-0 text-gray-700">ច្រោះទិន្នន័យ៖</h4>
        <div class="row">
            <div class="col-md-3">
                <!-- User Input Fields for Filtering -->
                <input class="form-control my-2 py-2" v-model="tempFilters.schoolName" @keydown.enter="applyFilter"
                    placeholder="អង្គភាព" />
            </div>

            <div class="col-md-3">
                <!-- <input class="form-control" v-model="tempFilters.province" @keydown.enter="applyFilter"
                    placeholder="រាជធានី ខេត្ត" /> -->
                <!-- <input class="form-control" v-model="tempFilters.type" @keydown.enter="applyFilter" placeholder="ប្រភេទសាលា" /> -->
                <select class="form-select my-2 py-2" v-model="tempFilters.province" aria-label="Select example">
                    <option value="">-- រាជធានី ខេត្ត --</option>
                    <option v-for="province in provinceData" :value="province">{{ province }}</option>
                </select>
            </div>

            <div class="col-md-3">
                <!-- <input class="form-control" v-model="tempFilters.type" @keydown.enter="applyFilter" placeholder="ប្រភេទសាលា" /> -->
                <select class="form-select my-2 py-2" v-model="tempFilters.type" aria-label="Select example">
                    <option value="">-- ប្រភេទសាលា --</option>
                    <option v-for="type in schoolType" :value="type">{{ type }}</option>
                </select>
            </div>

            <div class="col-md-3 d-flex justify-content-between align-items-center">
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
            <div class="d-flex ">
                <u>ទិន្នន័យ</u>៖ {{ filteredData.length }}/{{ schoolData.length }}
                <div><a href="https://drive.google.com/file/d/1DinD0TA2Xu32_p2lA9YhgdGSCFktGqXI/view?usp=sharing"
                        target="_blank" class="text-muted">&nbsp;(បញ្ជីសាលា) </a></div>
            </div>
            <div class="table-responsive">
                <table class="table table-striped text-nowrap">
                    <thead>
                        <tr class="fs-6 text-gray-800 border-bottom-2 border-gray-200">
                            <th>ល.រ</th>
                            <th class="">រាជធានី ខេត្ត</th>
                            <th class="">អង្គភាព</th>
                            <th class="">ប្រភេទសាលា</th>
                            <th class="min-w-100px">ព្រឹត្តិបត្រព័ត៌មាន</th>
                            <th class="min-w-100px">របាយការណ៍អធិការកិច្ច</th>
                            <th class="min-w-100px">ស្វ័យវាយតម្លៃ</th>
                            <th class="min-w-100px">ពិន្ទុ</th>
                            <th class="min-w-100px">ក្រុមការងារវាយតម្លៃ</th>
                            <th class="min-w-100px">ពិន្ទុ</th>
                            <th class="min-w-50px">ជាប់ស្ដង់ដាសាលាមធ្យមសិក្សាគំរូ ឆ្នាំ2024</th>
                            <th class="min-w-100px">សាលាប្រើប្រាស់ MIS</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(item, index) in filteredData" :key="item.id">
                            <td>{{ item.id }}</td>
                            <td>{{ item.province }}</td>
                            <td>{{ item.schoolName }}</td>
                            <td>{{ item.type }}</td>
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
import schoolType from '@/data/schoolType';

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
    type: '',
    modelSchoolStandardStatus: false
});

// Function to apply the temporary filter values to the actual filters on button click or Enter key press
const applyFilter = () => {
    filters.value = { ...tempFilters.value };
};

// Computed property to filter data based on the filters
const filteredData = computed(() => {
    return dataList.value.filter(item => {
        return (
            (!filters.value.schoolName || item.schoolName.toLowerCase().includes(filters.value.schoolName.toLowerCase())) &&
            (!filters.value.province || item.province.toLowerCase().includes(filters.value.province.toLowerCase())) &&
            (!filters.value.type || item.type.toLowerCase().includes(filters.value.type.toLowerCase())) &&
            (!filters.value.modelSchoolStandardStatus || item.modelSchoolStandardStatus === filters.value.modelSchoolStandardStatus)
        );
    });
});
</script>
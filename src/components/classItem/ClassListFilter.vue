<template>
    <div>
        <h1>Filter:</h1>
        <div class="row">
            <div class="col-md-3">
                <!-- User Input Fields for Filtering -->
                <input class="form-control" v-model="tempFilters.schoolName" @keydown.enter="applyFilter"
                    placeholder="អង្គភាព" />
            </div>
            <div class="col-md-3">
                <!-- <input class="form-control" v-model="tempFilters.province" @keydown.enter="applyFilter"
                    placeholder="រាជធានី ខេត្ត" /> -->
                <!-- <input class="form-control" v-model="tempFilters.type" @keydown.enter="applyFilter" placeholder="ប្រភេទសាលា" /> -->
                <select class="form-select" v-model="tempFilters.province" aria-label="Select example">
                    <option value="">-- រាជធានី ខេត្ត --</option>
                    <option value="ភ្នំពេញ">ភ្នំពេញ</option>
                    <option value="បាត់ដំបង">បាត់ដំបង</option>
                    <option value="កំពង់ស្ពឺ">កំពង់ស្ពឺ</option>
                </select>
            </div>
            <div class="col-md-3">
                <!-- <input class="form-control" v-model="tempFilters.type" @keydown.enter="applyFilter" placeholder="ប្រភេទសាលា" /> -->
                <select class="form-select" v-model="tempFilters.type" aria-label="Select example">
                    <option value="">-- ប្រភេទសាលា --</option>
                    <option value="ធនធាន">ធនធាន</option>
                    <option value="បណ្ដាញ">បណ្ដាញ</option>
                    <option value="ធម្មតា">ធម្មតា</option>
                </select>
            </div>
            <div class="col-md-3 d-flex justify-content-between align-items-center">
                <!-- Checkbox for Model School Standard Status -->
                <div class="form-check">
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
                <button class="btn btn-sm btn-light-primary" @click="applyFilter">Filter</button>

            </div>
        </div>
    </div>

    <!-- Filtered Results -->
    <div class="card mt-5">
        <div class="card-body">
            <div class="table-responsive">
                <table class="table table-striped gy-7 gs-7">
                    <thead>
                        <tr class="fs-6 text-gray-800 border-bottom-2 border-gray-200">
                            <th>ល.រ</th>
                            <th class="">អង្គភាព</th>
                            <th class="text-nowrap">រាជធានី ខេត្ត</th>
                            <th class="text-nowrap">ប្រភេទសាលា</th>
                            <th class="min-w-100px">ព្រឹត្តិបត្រព័ត៌មាន</th>
                            <th class="min-w-100px">ដើមឆ្នាំ</th>
                            <th class="min-w-100px">ចុងឆ្នាំ</th>
                            <th class="min-w-100px">ជាប់ស្ដង់ដាសាលាមធ្យមសិក្សាគំរូ ឆ្នាំ2024</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(item, index) in filteredData" :key="item.id">
                            <td>{{ index + 1 }}</td>
                            <td>{{ item.schoolName }}</td>
                            <td>{{ item.province }}</td>
                            <td>{{ item.type }}</td>
                            <td><a :href="item.profileLink" target="_blank">Profile Link</a></td>
                            <td><a :href="item.evalEarlyYearLink" target="_blank">Evaluation Early Year Link</a></td>
                            <td><a :href="item.evalEndYearLink" target="_blank">Evaluation End Year Link</a></td>
                            <td>{{ item.modelSchoolStandardStatus ? 'ជាប់' : 'មិនជាប់' }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

// Sample data
const dataList = ref([
    {
        id: 1,
        schoolName: 'វិ.កខគ',
        province: 'ភ្នំពេញ',
        type: 'ធនធាន',
        profileLink: 'https://example.com/maple-profile',
        evalEarlyYearLink: 'https://example.com/maple-early',
        evalEndYearLink: 'https://example.com/maple-end',
        modelSchoolStandardStatus: true
    },
    {
        id: 2,
        schoolName: 'អនុវិ.ងចឆ',
        province: 'បាត់ដំបង',
        type: 'បណ្ដាញ',
        profileLink: 'https://example.com/westwood-profile',
        evalEarlyYearLink: 'https://example.com/westwood-early',
        evalEndYearLink: 'https://example.com/westwood-end',
        modelSchoolStandardStatus: false
    },
    {
        id: 2,
        schoolName: 'វិ. ថង',
        province: 'កំពង់ស្ពឺ',
        type: 'ធម្មតា',
        profileLink: 'https://example.com/westwood-profile',
        evalEarlyYearLink: 'https://example.com/westwood-early',
        evalEndYearLink: 'https://example.com/westwood-end',
        modelSchoolStandardStatus: false
    }
]);

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
<template>
  <div class="skills-chart">
    <vue-frappe
      ref="languageChart"
      id="language"
      :labels="filteredLabels"
      title="Programming Language Growth Chart"
      type="bar"
      :height="300"
      :colors="colors"
      :dataSets="filteredLanguageData"
      :tooltipOptions="tooltipOptions">
    </vue-frappe>
    <vue-frappe
      id="frameworks"
      :labels="filteredLabels"
      title="Framework Growth Chart"
      type="bar"
      :height="300"
      :colors="colors"
      :tooltipOptions="tooltipOptions"
      :dataSets="filteredFrameworkData">
    </vue-frappe>
    <vue-frappe
      id="software"
      :labels="filteredLabels"
      title="Tooling Growth Chart"
      type="bar"
      :height="300"
      :colors="colors"
      :tooltipOptions="tooltipOptions"
      :dataSets="filteredSoftwareData">
    </vue-frappe>
  </div>
</template>
<script>
import resumeData from '@/data/resume'
const labels = [
    '2011', '2012', '2013', '2014',
    '2015', '2016', '2017', '2018', '2019', '2020'
]

const colors = ['purple', '#ffa3ef', 'light-blue', 'green', 'blue', 'red', 'orange', 'purple']
export default {
  name: 'SkillsChart',
  props: {
    startYear: {
        type: Number
    },
    endYear: {
        type: Number
    }
  },
  computed: {
    tooltipOptions () {
		return {
            formatTooltipX: d => (d + '').toUpperCase(),
            formatTooltipY: d => d + '%',
        }
	},
      filteredIndices () {
          let start = 0
          let end = this.labels.length - 1
        while (this.labels[start] < (this.startYear || 2000)  || this.labels[end] > (this.endYear || 2040)) {
            if (this.labels[end] > this.endYear) end--
            if (this.labels[start] < this.startYear ) start++
        }
        return [start, end]
      },
      filteredLabels () {
          let [start, end] = this.filteredIndices
          if (start === undefined || end === undefined) return this.labels
          return this.labels.slice(start, end+1)
      },
      filteredLanguageData () {
          let [start, end] = this.filteredIndices
          return this.languageChartData.map(d => {
              return {
                  ...d,
                  values: d.values.slice(start, end + 1)
              }
          })
      },
      filteredFrameworkData () {
          let [start, end] = this.filteredIndices
          return this.frameworkChartData.map(d => {
              return {
                  ...d,
                  values: d.values.slice(start, end + 1)
              }
          })
      },
      filteredSoftwareData () {
          let [start, end] = this.filteredIndices
          return this.softwareChartData.map(d => {
              return {
                  ...d,
                  values: d.values.slice(start, end + 1)
              }
          })
      },

  },
  data () {
      return {
        colors,
        labels,
        languageChartData: [{
              name: "Java", chartType: 'line',
              values: [0, 30, 60, 80, 70, 65, 60, 55, 60, 65]
          }, 
          {
              name: "JavaScript", chartType: 'line',
              values: [0, 10, 50, 70, 75, 85, 90, 95, 95, 100]
          },
          {
              name: "Ruby", chartType: 'line',
              values: [0, 20, 50, 60, 80, 90, 95, 95, 90, 90]
          },
          {
              name: "Python", chartType: 'line',
              values: [0, 5, 5, 10, 30, 40, 45, 55, 65, 75]
          }
        ],
        frameworkChartData: [{
              name: "Express.js", chartType: 'line',
              values: [0, 0, 5, 5, 40, 75, 80, 85, 85, 90]
          }, 
          {
              name: "Vue.js", chartType: 'line',
              values: [0, 0, 0, 0, 0, 0, 0, 70, 85, 95]
          },
          {
              name: "Node.js", chartType: 'line',
              values: [0, 0, 5, 10, 50, 80, 85, 90, 90, 95]
          },
          {
              name: "Ruby on Rails", chartType: 'line',
              values: [5, 15, 55, 70, 85, 90, 95, 90, 85, 90]
          },
          {
              name: "Sinatra", chartType: 'line',
              values: [5, 15, 25, 30, 50, 60, 45, 45, 50, 50]
          },
          {
              name: "Polymer.js", chartType: 'line',
              values: [0, 0, 0, 0, 30, 60, 80, 85, 55, 40]
          },
          {
              name: "Meteor.js", chartType: 'line',
              values: [0, 5, 15, 45, 65, 80, 85, 70, 65, 65]
          },
          {
              name: "Nuxt.js", chartType: 'line',
              values: [0, 0, 0, 0, 0, 0, 0, 70, 85, 90]
          }
        ],
        softwareChartData: [{
              name: "Adobe CC Suite", chartType: 'line',
              values: [40, 60, 80, 85, 90, 85, 85, 80, 85, 90]
          }, 
          {
              name: "Sketch", chartType: 'line',
              values: [0, 0, 15, 30, 40, 50, 55, 60, 55, 60]
          },
          {
              name: "Jupyter Notebook", chartType: 'line',
              values: [0, 0, 0, 0, 0, 0, 60, 75, 80, 85]
          },
          {
              name: "Visual Studio Code", chartType: 'line',
              values: [0, 0, 0, 0, 0, 0, 65, 70, 85, 90]
          },
          {
              name: "New Relic", chartType: 'line',
              values: [0, 0, 0, 30, 50, 75, 65, 70, 70, 75]
          },
          {
              name: "Git", chartType: 'line',
              values: [40, 60, 80, 85, 85, 90, 95, 95, 95, 95]
          },
          {
              name: "Agile (Jira)", chartType: 'line',
              values: [10, 25, 40, 60, 75, 75, 80, 80, 85, 90]
          }
        ],
      }
  },
}
</script>
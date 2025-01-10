<template>
    <div>
      <ejs-kanban id="KanbanBoard-" keyField="Status" :dataSource="data" :cardSettings="cardSettings"
          :swimlaneSettings="swimlaneSettings" :dialogSettings="dialogSettings">
          <e-columns>
              <e-column headerText="To do" keyField="To do"></e-column>
              <e-column headerText="In Progress" keyField="InProgress"></e-column>
              <e-column headerText="In Review" keyField="Review"></e-column>
              <e-column headerText="Done" keyField="Close"></e-column>
          </e-columns>
          <template #dialogTemplate="{data}">
              <table>
                  <tbody>
                      <tr>
                          <td>ID</td>
                          <td>
                              <input id="Id" name="Id" type="text" v-model="data.Id" class="e-input" disabled />
                          </td>
                      </tr>
                      <tr>
                          <td>Status</td>
                          <td>
                              <ejs-dropdownlist :dataSource="statusData" id="Status" name="Status" v-model="data.Status"
                              placeholder="Status" cssClass="e-field"></ejs-dropdownlist>
                          </td>
                      </tr>
                      <tr>
                          <td>Assignee</td>
                          <td>
                              <ejs-dropdownlist :dataSource="assigneeData" id="Assignee" name="Assignee" v-model="data.Assignee" placeholder="=Assignee" cssClass="e-field"></ejs-dropdownlist>
                          </td>
                      </tr>
                      <tr>
                          <td>Summary</td>
                          <td>
                              <div class="e-float-input">
                                  <textarea id="Summary" name="Summary" type="text" v-model="data.Summary" class="e-input"></textarea>
                              </div>
                          </td>
                      </tr>
                  </tbody>
              </table>
          </template>
      </ejs-kanban>
  
      <div v-if="!$auth.loading">
        <!-- show login when not authenticated -->
        <a v-if="!$auth.isAuthenticated" @click="login">Log in</a>
        <!-- show logout when authenticated -->
        <a v-if="$auth.isAuthenticated" @click="logout">Log out</a>
      </div>
    </div>
  </template>
  
<script>

import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-vue-kanban";
import { DropDownListComponent} from "@syncfusion/ej2-vue-dropdowns";
export default {
    components: {
        "ejs-kanban": KanbanComponent,
        "e-columns": ColumnsDirective,
        "e-column": ColumnDirective,
        "ejs-dropdownlist": DropDownListComponent
    },
    data: function () {
        return {
            data: [
                {
                    "Id": "ภารกิจ 1",
                    "Title": "Task - 29001",
                    "Status": "To do",
                    "Summary": "แก้ไขรายชื่อลูกค้า",
                    "Tags": "Analyze,Customer",
                    "Estimate": 3.5,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 1,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-low, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 2",
                    "Title": "Task - 29002",
                    "Status": "InProgress",
                    "Summary": "พัฒนาคุณภาพแอป",
                    "Tags": "Improvement",
                    "Estimate": 6,
                    "Assignee": "ศุภกร วรรณประสิทธิ์",
                    "RankId": 1,
                    "Color": "#673AB8",
                    "ClassName": "e-improvement, e-normal, e-andrew-fuller"
                },
                {
                    "Id": "ภารกิจ 3",
                    "Title": "Task - 29003",
                    "Status": "To do",
                    "Summary": "จัดประชุมออนไลน์กับลูกค้าเพื่อรับข้อกำหนดใหม่",
                    "Tags": "Meeting",
                    "Estimate": 5.5,
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 2,
                    "Color": "#1F88E5",
                    "ClassName": "e-others, e-critical, e-janet-leverling"
                },
                {
                    "Id": "ภารกิจ 4",
                    "Title": "Task - 29004",
                    "Status": "InProgress",
                    "Summary": "แก้ไขปัญหาที่แจ้งในระบบ IE browser",
                    "Tags": "IE",
                    "Estimate": 2.5,
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 2,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-release, e-janet-leverling"
                },
                {
                    "Id": "ภารกิจ 5",
                    "Title": "Task - 29005",
                    "Status": "Review",
                    "Summary": "แก้ไขปัญหาที่ลูกค้าแจ้งมา",
                    "Tags": "Customer",
                    "Estimate": "3.5",
                    "Assignee": "ชลธิชา ยศพร",
                    "RankId": 1,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-low, e-steven-walker"
                },
                {
                    "Id": "ภารกิจ 6",
                    "Title": "Task - 29007",
                    "Status": "Review",
                    "Summary": "ตรวจสอบความถูกต้องของข้อกำหนดใหม่",
                    "Tags": "Validation",
                    "Estimate": 1.5,
                    "Assignee": "ปรียานุช หอมเสียง",
                    "RankId": 1,
                    "Color": "#673AB8",
                    "ClassName": "e-improvement, e-low, e-robert-king"
                },
                {
                    "Id": "ภารกิจ 7",
                    "Title": "Task - 29009",
                    "Status": "Review",
                    "Summary": "ตรวจสอบปัญหาที่ลูกค้ารายงานใน Safari browser ",
                    "Tags": "Fix,Safari",
                    "Estimate": 1.5,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 2,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-release, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 8",
                    "Title": "Task - 29010",
                    "Status": "Close",
                    "Summary": "ทดสอบแอปใน IE browser",
                    "Tags": "Review,IE",
                    "Estimate": 5.5,
                    "Assignee": "พิชชาพร อารยะไกร",
                    "RankId": 3,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-low, e-margaret-hamilt"
                },
                {
                    "Id": "ภารกิจ 9",
                    "Title": "Task - 29011",
                    "Status": "Review",
                    "Summary": "ตรวจสอบปัญหาที่ลูกค้ารายงาน",
                    "Tags": "Validation,Fix",
                    "Estimate": 1,
                    "Assignee": "ชลธิชา ยศพร",
                    "RankId": 1,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-high, e-steven-walker"
                },
                {
                    "Id": "ภารกิจ 10",
                    "Title": "Task - 29015",
                    "Status": "To do",
                    "Summary": "แสดงข้อมูลที่ดึงมาจากเซิร์ฟเวอร์ใน grid control",
                    "Tags": "Database,SQL",
                    "Estimate": 5.5,
                    "Assignee": "พิชชาพร อารยะไกร",
                    "RankId": 4,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-high, e-margaret-hamilt"
                },
                {
                    "Id": "ภารกิจ 11",
                    "Title": "Task - 29016",
                    "Status": "InProgress",
                    "Summary": "แก้ไขปัญหาที่เกิดขึ้นเมื่อ SQL Server ไม่สามารถเปิดฐานข้อมูลเริ่มต้นที่กำหนดไว้สำหรับผู้ใช้",
                    "Tags": "Database,Sql2008",
                    "Estimate": 2.5,
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 4,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-critical, e-janet-leverling"
                },
                {
                    "Id": "ภารกิจ 12",
                    "Title": "Task - 29017",
                    "Status": "Review",
                    "Summary": "แก้ไขปัญหาจากรายงานของdata binding",
                    "Tags": "Databinding",
                    "Estimate": "3.5",
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 4,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-normal, e-janet-leverling"
                },
                {
                    "Id": "ภารกิจ 13",
                    "Title": "Task - 29018",
                    "Status": "Close",
                    "Summary": "จัดการระบบการเชื่อมต่อ SQL server 2008",
                    "Tags": "Grid,Sql",
                    "Estimate": 2,
                    "Assignee": "ศุภกร วรรณประสิทธิ์",
                    "RankId": 4,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-release, e-andrew-fuller"
                },
                {
                    "Id": "ภารกิจ 14",
                    "Title": "Task - 29019",
                    "Status": "To do",
                    "Summary": "แก้ไขปัญหาที่รายงานเกี่ยวกับการผูกข้อมูล",
                    "Tags": "Validation",
                    "Estimate": 1.5,
                    "Assignee": "พิชชาพร อารยะไกร",
                    "RankId": 1,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-low, e-margaret-hamilt"
                },
                {
                    "Id": "ภารกิจ 15",
                    "Title": "Task - 29020",
                    "Status": "Close",
                    "Summary": "จัดการgrid control",
                    "Tags": "Analyze",
                    "Estimate": 2.5,
                    "Assignee": "พิชชาพร อารยะไกร",
                    "RankId": 5,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-high, e-margaret-hamilt"
                },
                {
                    "Id": "ภารกิจ 16",
                    "Title": "Task - 29021",
                    "Status": "Close",
                    "Summary": "สร้างสคริปต์ Stored Procedure สำหรับการผูกข้อมูลเริ่มต้นให้กับตาราง (Grid)",
                    "Tags": "Databinding",
                    "Estimate": 1.5,
                    "Assignee": "ชลธิชา ยศพร",
                    "RankId": 6,
                    "Color": "#1F88E5",
                    "ClassName": "e-others, e-release, e-steven-walker"
                },
                {
                    "Id": "ภารกิจ 17",
                    "Title": "Task - 29022",
                    "Status": "Close",
                    "Summary": "จัดการระบบstored procedures",
                    "Tags": "Procedures",
                    "Estimate": 5.5,
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 7,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-release, e-janet-leverling"
                },
                {
                    "Id": "ภารกิจ 18",
                    "Title": "Task - 29023",
                    "Status": "To do",
                    "Summary": "แก้ปัญหาระบบการแก้ไข",
                    "Tags": "Editing",
                    "Estimate": 1,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 1,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-critical, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 19",
                    "Title": "Task - 29024",
                    "Status": "Review",
                    "Summary": "ทดสอบฟังก์ชันแก้ไข",
                    "Tags": "Editing,Test",
                    "Estimate": 0.5,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 5,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-normal, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 20",
                    "Title": "Task - 29025",
                    "Status": "To do",
                    "Summary": "พัฒนาคุณภาพระบบแก้ไข",
                    "Type": "Improvement",
                    "Tags": "Editing",
                    "Estimate": 3.5,
                    "Assignee": "ศุภกร วรรณประสิทธิ์",
                    "RankId": 5,
                    "Color": "#673AB8",
                    "ClassName": "e-improvement, e-low, e-andrew-fuller"
                },
                {
                    "Id": "ภารกิจ 21",
                    "Title": "Task - 29026",
                    "Status": "InProgress",
                    "Summary": "พัฒนาคุณภาพฟังก์ชันการแก้ไข",
                    "Tags": "Performance",
                    "Estimate": 6,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 5,
                    "Color": "#e91e64",
                    "ClassName": "e-epic, e-high, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 22",
                    "Title": "Task - 29027",
                    "Status": "To do",
                    "Summary": "นัดประชุมกับลูกค้าเพื่อโชว์เดโม่",
                    "Tags": "Meeting,Editing",
                    "Estimate": 5.5,
                    "Assignee": "ชลธิชา ยศพร",
                    "RankId": 6,
                    "Color": "#1F88E5",
                    "ClassName": "e-others, e-high, e-steven-walker"
                },
                {
                    "Id": "ภารกิจ 23",
                    "Title": "Task - 29029",
                    "Status": "Review",
                    "Summary": "จัดการระบบการแก้ไขที่ลูกค้ารายงานมา",
                    "Tags": "Editing,Fix",
                    "Estimate": "3.5",
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 6,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-low, e-janet-leverling"
                },
                {
                    "Id": "ภารกิจ 24",
                    "Title": "Task - 29030",
                    "Status": "To do",
                    "Summary": "แก้ไขข้อมูลที่ลูกค้ารายงานเข้ามา",
                    "Type": "Bug",
                    "Tags": "Customer",
                    "Estimate": "3.5",
                    "Assignee": "ชลธิชา ยศพร",
                    "RankId": 1,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-critical, e-steven-walker"
                },
                {
                    "Id": "ภารกิจ 25",
                    "Title": "Task - 29031",
                    "Status": "To do",
                    "Summary": "แก้ไขปัญหาที่รายงานในเบราว์เซอร์ Safari",
                    "Tags": "Fix,Safari",
                    "Estimate": 1.5,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 2,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-release, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 26",
                    "Title": "Task - 29032",
                    "Status": "InProgress",
                    "Summary": "ตรวจสอบการตรวจสอบความถูกต้องของหน้าเข้าสู่ระบบ",
                    "Tags": "Testing",
                    "Estimate": 0.5,
                    "Assignee": "พิชชาพร อารยะไกร",
                    "RankId": 3,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-release, e-michael-suyama"
                },
                {
                    "Id": "ภารกิจ 27",
                    "Title": "Task - 29033",
                    "Status": "Close",
                    "Summary": "แก้ไขปัญหา data binding",
                    "Tags": "Databinding",
                    "Estimate": "3.5",
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 4,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-normal, e-janet-leverling"
                },
                {
                    "Id": "Task 28",
                    "Title": "Task - 29034",
                    "Status": "To do",
                    "Summary": "ทดสอบฟังก์ชันระบบการแก้ไข",
                    "Tags": "Editing,Test",
                    "Estimate": 0.5,
                    "Assignee": "ธนัชชา พงษ์ศักดิ์",
                    "RankId": 5,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-normal, e-nancy-davloio"
                },
                {
                    "Id": "ภารกิจ 29",
                    "Title": "Task - 29035",
                    "Status": "Close",
                    "Summary": "แก้ปัญหาระบบขัดข้องFirefox",
                    "Tags": "Editing,Fix",
                    "Estimate": 1.5,
                    "Assignee": "ปรียานุช หอมเสียง",
                    "RankId": 7,
                    "Color": "#E64A19",
                    "ClassName": "e-bug, e-critical, e-robert-king"
                },
                {
                    "Id": "ภารกิจ 30",
                    "Title": "Task - 29036",
                    "Status": "Close",
                    "Summary": "ทดสอบระบบการแก้ไขใน IE browser",
                    "Tags": "Testing",
                    "Estimate": 5.5,
                    "Assignee": "อารยา จันทรโสภา",
                    "RankId": 10,
                    "Color": "#02897B",
                    "ClassName": "e-story, e-normal, e-janet-leverling"
                }
            ],
            statusData: ["To do", "InProgress", "Review", "Close"],
            assigneeData: ["ธนัชชา พงษ์ศักดิ์","ศุภกร วรรณประสิทธิ์","อารยา จันทรโสภา","ชลธิชา ยศพร","ปรียานุช หอมเสียง","พิชชาพร อารยะไกร"],

            
            cardSettings: {
                contentField: "Summary",
                headerField: "Id",
            },
            swimlaneSettings: {
                keyField: "Assignee"
            },
            dialogSettings:{
                template: "dialogTemplate"
            }
        }
    }
},
  methods: {
    // Log the user in
    login() {
      this.$auth.loginWithRedirect();
    },
    // Log the user out
    logout() {
      this.$auth.logout({
        returnTo: window.location.origin,
      });
    }
  };
</script>

<style>
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-layouts/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-vue-kanban/styles/material.css';
</style>
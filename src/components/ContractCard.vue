<script setup>
const props = defineProps({
  project: Object,
});
const project = props.project;
let date = new Date(project.updated_timestmp);
let dateString = `${date.getMonth()}.${date.getDay()}.${date.getFullYear()}`;
let color = "#9F9F9F";
let stageClassName = `stage ${project.projectState
  .toLowerCase()
  .replaceAll(" ", "-")}`;
</script>

<template>
  <div class="contract">
    <div class="contract-header">
      <div class="customerName">{{ project.customerName || "Untitled" }}</div>
      <div class="projectId">ID: {{ project.projectId }}</div>
    </div>
    <div class="contract-main">
      <div class="address">{{ project.address }}</div>
      <div class="rooms">
        <div v-for="room in project.rooms" :key="room.id" class="room">
          {{ room.name }}
        </div>
      </div>

      <div class="details">
        <div className="detail-title">
          <div :style="{ color: color }">Last updated</div>
          <div class="last-update">{{ dateString }}</div>
        </div>
        <div className="detail-title">
          <div :style="{ color: color }">Total</div>
          <div class="total">
            {{
              project.totalProject.toLocaleString("en-US", {
                maximumFractionDigits: 2,
                minimumFractionDigits: 2,
              })
            }}
          </div>
        </div>
        <div className="detail-title">
          <div :style="{ color: color }">Stage</div>
          <div :class="stageClassName">{{ project.projectState }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped land="scss">
.contract {
  width: 350px;
  background: #ffffff;
  border: 1px solid #ddedf4;
  border-radius: 9px;
  display: flex;
  flex-direction: column;

  .contract-header {
    background: #f6f9fa;
    height: 76px;
    padding-left: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;

    .customerName {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      max-width: 80%;
      margin-bottom: 5px;
      font-weight: 700;
      font-size: 16px;
      line-height: 20px;
      letter-spacing: 0.272728px;
      color: #2d2d2d;
    }

    .projectId {
      font-weight: 400;
      font-size: 12px;
      line-height: 12px;
      letter-spacing: 0.272728px;
      color: #2d2d2d;
      opacity: 0.5;
    }
  }
  .contract-main {
    height: 159px;
    padding-left: 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;

    .address {
      font-weight: 400;
      font-size: 14px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      max-width: 80%;
    }
    .rooms {
      display: flex;
      justify-content: start;
      gap: 3px;

      .room {
        font-weight: 400;
        font-size: 12px;
        line-height: 20px;
        letter-spacing: 0.272728px;
        color: #3cb2e4;
        background: rgba(60, 178, 228, 0.1);
        border-radius: 6px;
        height: 28px;
        padding: 4px 10px;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }
    .details {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      margin-right: 20px;

      .total {
        font-weight: 700;
      }
      .stage {
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50px;
        width: fit-content;
        padding: 0 10px;
      }
    }
  }
}

.stage.in-progress {
  background: #f6f9fa;
}

.stage.done {
  color: #30d869;
  background: #ebfcec;
}

.stage.cancelled {
  color: #3cb2e4;
  background: #ebf7fc;
}

.stage.negotiation {
  color: #e4783c;
  background: #faeee8;
}
</style>

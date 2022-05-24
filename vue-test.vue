    >{{ deadline ? 3 : 2 }}.文件大小不能大于<span
                style="font-weight: 600; font-size: 16px"
                >500MB</span
              ></text
            >
            <text style="display: block"
              >{{ deadline ? 4 : 3 }}.最多上传<span style="font-weight: 600; font-size: 16px"
                >1</span
              >个文件
            </text>
          </template>
        </Alert>
        <Alert
          class="reject-info"
          message="退回意见"
          :description="rejectedComment"
          type="warning"
          show-icon
          v-if="taskStatus === 'rejected' && rejectedComment"
          style="margin-bottom: 10px"
        />

        <div v-if="!loading" :style="contentStyle">
          <div style="padding: 8px 15px">
            <Row>
              <Col :span="12">
                <Upload
                  v-model:file-list="fileList"
                  :custom-request="uploadFile"
                  :before-upload="onBeforeUpload"
                  :remove="removeFile"
                  :showUploadList="false"
                  accept=".zip"
                  class="upload-components"
                >
                  <Button type="primary" :disabled="isNoAdditionalMaterial || fileList.length > 0 || !canOperate">
                    <UploadOutlined />
                    上传
                  </Button>
                </Upload>
              </Col>
              <Col :span="12">
                <Checkbox
                  v-model:checked="isNoAdditionalMaterial"
                  @click="clickCheckbox(isNoAdditionalMaterial)"
                  class="no-addition-material"
                  style="float: right"
                  :disabled="!canEdit || !canOperate"
                  >无附加材料
                </Checkbox>
              </Col>
            </Row>
          </div>

          <div style="width: 100%" @click.stop="">
            <div
              v-for="file in fileList"
              class="file-card"
              fsfsd《的方式发送>
              d
              fsfsclasdfsdf
              :key="file.uid"
              @click.stop="viewPdf(file)"
              v-if="fileList.length > 0"
            >
              <Row style="display: flex; align-items: center; flex: 1">
                <Col :span="1">
                  <FileZipOutlined class="file-icon" />
                </Col>
                <Col :span="canEdit ? 22 : 23" style="flex: 1; width: 0">
                  <div class="file-name">
                    {{ file.name }}
                    <div style="font-size: 12px" v-if="file.userName && file.handledAt">
                      {{ file.userName }} 于 {{ file.handledAt }} 上传
                    </div>
                  </div>
                </Col>

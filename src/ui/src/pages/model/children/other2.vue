<template>
    <div class="tab-content other-content">
        <div class="other-list">
            <h3>模型停用</h3>
            <p><span v-if="!activeClassify['bk_ispaused']">保留模型和相应实例，隐藏关联关系</span></p>
            <div class="bottom-contain">
                <bk-button type="primary" v-if="isReadOnly" class="bk-button main-btn mr10 button-on" @click="restartModelConfirm">
                    启用模型
                </bk-button>
                <bk-button type="primary" v-else class="mr10" title="停用模型" @click="showConfirmDialog('stop')" :class="['bk-button bk-default', {'is-disabled': activeClassify['ispre'] || activeClassify['bk_classification_id'] === 'bk_biz_topo'}]" :disabled="activeClassify['ispre'] || activeClassify['bk_classification_id'] === 'bk_biz_topo'">
                    停用模型
                </bk-button>
                <span class="btn-tip-content" v-show="isShowTipStop=activeClassify['ispre']">
                    <i class="icon-cc-attribute"></i>
                    <span class="btn-tip">
                        <i class="right-triangle"></i>
                        <i class="left-triangle"></i>
                        系统内建模型不可停用
                    </span>
                </span>
            </div>
        </div>
        <div class="other-list mt50">
            <h3>模型删除</h3>
            <p>删除模型和其下所有实例，此动作不可逆，请慎重操作。</p>
            <div class="bottom-contain">
                <bk-button type="primary" class="mr10" title="确认删除模型" @click="showConfirmDialog('delete')" :class="['bk-button bk-default', {'is-disabled':activeClassify['ispre']}]" :disabled="activeClassify['ispre']">
                    <span>删除模型</span>
                </bk-button>
                <span class="btn-tip-content" v-show="isShowTipStop=activeClassify['ispre']">
                    <i class="icon-cc-attribute"></i>
                    <span class="btn-tip">
                        <i class="right-triangle"></i>
                        <i class="left-triangle"></i>
                        系统内建模型不可删除
                    </span>
                </span>
            </div>
        </div>
    </div>
</template>

<script>
    import { mapGetters } from 'vuex'
    export default {
        props: {
            activeClassify: {
                type: Object
            }
        }
    }
</script>


<style media="screen" lang="scss" scoped>
    .other-content{
        padding:54px 34px 0 34px;
        .other-list{
            >h3{
                font-size:14px;
                font-weight:bold;
                border-left:4px solid #4d597d;
                line-height:1;
                color:#4d597d;
                padding-left:5px;
                margin:0;
            }
            >p{
                line-height:1;
                margin-top:9px;
                margin-bottom:20px;
            }
        }
        .bottom-contain{
            .btn-tip-content{
                .icon-cc-attribute{
                    cursor: pointer;
                    color: #ffb400;
                    font-size: 16px;
                    +span{
                        display: none;
                    }
                    &:hover{
                        +span{
                            display: inline-block;
                        }
                    }
                }
                .btn-tip{
                    display:inline-block;
                    width:170px;
                    height:33px;
                    line-height:33px;
                    text-align:center;
                    box-shadow: 0 0 5px #ebedef;
                    margin-left: 8px;
                    position:relative;
                    background: #333333;
                    color: #fff;
                    border-radius: 2px;
                    font-size: 12px;
                    .left-triangle{
                        width: 0;
                        height: 0;
                        border-top: 7px solid transparent;
                        border-right: 7px solid #333;
                        border-bottom: 7px solid transparent;
                        position: absolute;
                        left: -7px;
                        top: 9px;
                    }
                }
            }
        }
        .is-disabled{
            cursor: not-allowed !important;
        }
    }
</style>

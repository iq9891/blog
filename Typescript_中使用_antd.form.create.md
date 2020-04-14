# Typescript 中使用 antd.form.create

Typescript 中使用 antd.form.create ，总是报错，经多方查找学习，记录如下问题及解决方案。

## 报错内容如下

```
TS2322: Type '{ dataSource: any[]; variableSource: any[]; chosenType: string; isMultiple: boolean; onAddConfigValue: () => void; hasRelatedComponent: boolean; onChangeRelatedComponent: (status: any) => void; onChangeConfigValueStatus: (id: any) => () => void; onUpdateConfigValue: (id: any) => () => void; onDeleteConfigValue: (id:...' is not assignable to type 'IntrinsicAttributes & IntrinsicClassAttributes<Component<Pick<FormComponentProps<any>, "wrappedComponentRef">, any, any>> & Readonly<...> & Readonly<...>'.
  Property 'dataSource' does not exist on type 'IntrinsicAttributes & IntrinsicClassAttributes<Component<Pick<FormComponentProps<any>, "wrappedComponentRef">, any, any>> & Readonly<...> & Readonly<...>'.
```

## 解决办法如下：

1. `import {FormComponentProps} from 'antd/lib/form/Form';`

2.
```
interface CreateNoticeModalProps extends FormComponentProps {
  isShow: boolean
  onCancel: any
  onOk: any
}
```

3. `class Test extends React.Component<CreateNoticeModalProps{}> {}`

4. 最关键的
`export default Form.create<CreateNoticeModalProps>()(CreateNoticeModal)`

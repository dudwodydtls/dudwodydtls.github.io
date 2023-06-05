---
layout: single
title: "redux/toolkit"
categories: coding
tag: [redux/toolkit]
toc: true
author_profile: false
sidebar:
 nav: "docs"
typora-root-url: ../
---

설치

(기존의 redux를 삭제해도 상관없음, redux-tookit에 포함되어있음)

```javascript
npm install @reduxjs/toolkit
```

reducer를 작성한다.

```javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
 productList: [],
 selecedItem: null
}

// createSlice에는 세 개의 매개변수가 들어가야 함
// name(관련된 하나의 단어), initialState, reducers(객체 안에 함수들이 들어있음)
 const productSlice = createSlice({
   name: "product",
   initialState,
   reducers:{
     addAllProduct(state, action) {
        state.productList = action.payload.data;
     },
    addSigleProduct(state, action) {
       state.selecedItem = action.payload;
    },
  },
})

export const SelectedItemSelector = () => (root) => root.product.selectedItem; // selectedItem을 감시하기 위해
export const productListSelector = () => (root) => root.product.productList; // productList를 감시하기 위해 
export const productActions = productSlice.actions; // 함수 사용
export default proeuctSlice.reducer;
```

store를 작성한다.

```javascript
import { configureStore } from '@reduxjs/toolkit';
import productReducer from './productReducer';

const store = configureStore({
   reducer:{
      product: productReducer,
   }
})

export default store;
```

사용하고자 하는 컴포넌트에서 활용한다.

```javascript
// 기존 : dispatch({ type: 'GET_PRODUCT_SUCCESS', payload: {data}});
// toolkit: dispatch(productActions.getAllProducts({data}))
import { useDispatch, useSelector } from 'react-redux';
import { productActions, productListSelector, selectedItemSelector } from './redux/productReducer';


const DispatchExComponent = () => {
   const dispatch = useDispatch();
   // useSelector로 감시하다가 변화를 감지하면 페이지를 reload한다.
   const productList = useSelector(productListSelector());
   const selectedItem = useSelector(selectedItemSelector());
   return (
      <div>
         <div onClick={() => dispatch(productActions.addAllProduct([1,2,3]))}>redux store의 product에 add</div>
         <div onClick={() => dispatch(productActions.addSigleProduct(1))}>redux store의 selectedItem에 add</div>
         <div onClick={() => console.log(productList)}>store의 productList 감시하기</div>
         <div onClick={() => console.log(selectedItem)}>store의 selectedItem 감시하기</div>
      </div>
   )
}

```


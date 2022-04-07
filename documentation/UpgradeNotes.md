Ng-Bootstrap Documentation
https://ng-bootstrap.github.io/#/components/nav/overview
https://ng-bootstrap.github.io/#/components/nav/examples


Upgrade the customization packages by replacing the ngb-tabset customization that is deprecated in ng-bootstrap 8 with the new ngb-navbar customization.
https://www.ibm.com/docs/en/store-engagement?topic=developing-upgrading-angular-11

Old ngb-tabset customization:
```
<ngb-tabset type="pills" (tabChange)="onTabChange($event)" [activeId]="activeTab">
  <ngb-tab id="product">
    <ng-template ngbTabTitle>
      <div id="product" [attr.tid]="componentId+'ProductsTitle'">
        <span translate
          [translateParams]="{count: shipmentLinesModel.ShipmentLines.TotalNumberOfRecords}">shipmentSummary.TITLE_Products</span>
        <span translate class="small font-weight-normal"
          [translateParams]="{unit: shipmentLinesModel.ShipmentLines.units}">shipmentSummary.LABEL_Units</span>
      </div>
    </ng-template>
    <ng-template ngbTabContent>
      <isf-shipment-summary-products *ngIf="showShipmentLineList" [pickRequestModel]="pickRequestModel"
        [data]="shipmentLinesModel.ShipmentLines.ShipmentLine" [visibleCount]="visibleCount">
      </isf-shipment-summary-products>
    </ng-template>
  </ngb-tab>
  <ngb-tab id="packages" *ngIf="containerDetails && containerDetails.TotalNumberOfRecords>0">
    <ng-template ngbTabTitle>
      <div id="packages" [attr.tid]="componentId+'PackagesTitle'">
        <span translate
          [translateParams]="{count: containerDetails.TotalNumberOfRecords}">shipmentSummary.TITLE_Packages</span>
      </div>
    </ng-template>
    <ng-template ngbTabContent>
      <isf-shipment-summary-packages *ngIf="showShipmentLineList" [packageList]="containerDetails"
        [visibleCount]="visibleCount" (refreshPackage)="refreshSummaryDetails($event)"
        [shipmentDetailsModel]="shipmentDetailsModel"></isf-shipment-summary-packages>
    </ng-template>
  </ngb-tab>
</ngb-tabset>
```

New ngb-navbar customization:
```
<ul ngbNav #shipmentSummaryPageTabSet="ngbNav" class="nav-pills pt-1 isf-font-size-14"
  (navChange)="onTabChange($event)" [activeId]="activeTab">
  <li [ngbNavItem]="'products'">
    <a class="nav-link" ngbNavLink [attr.tid]="componentId+'ProductsTitle'">
      <span translate
        [translateParams]="{count: shipmentLinesModel.ShipmentLines.TotalNumberOfRecords}">shipmentSummary.TITLE_Products</span>
      <span translate class="small font-weight-normal"
        [translateParams]="{unit: shipmentLinesModel.ShipmentLines.units}">shipmentSummary.LABEL_Units</span>
    </a>
    <ng-template ngbNavContent>
      <isf-shipment-summary-products *ngIf="showShipmentLineList" [pickRequestModel]="pickRequestModel"
        [data]="shipmentLinesModel.ShipmentLines.ShipmentLine" [visibleCount]="visibleCount">
      </isf-shipment-summary-products>
    </ng-template>
  </li>
  <li *ngIf="containerDetails && containerDetails.TotalNumberOfRecords>0" [ngbNavItem]="'packages'">
    <a class="nav-link" ngbNavLink [attr.tid]="componentId+'PackagesTitle'">
      <span translate
        [translateParams]="{count: containerDetails.TotalNumberOfRecords}">shipmentSummary.TITLE_Packages</span>
    </a>
    <ng-template ngbNavContent>
      <isf-shipment-summary-packages *ngIf="showShipmentLineList" [packageList]="containerDetails"
        [visibleCount]="visibleCount" (refreshPackage)="refreshSummaryDetails($event)"
        [shipmentDetailsModel]="shipmentDetailsModel"></isf-shipment-summary-packages>
    </ng-template>
  </li>
</ul>
<div [ngbNavOutlet]="shipmentSummaryPageTabSet" id="navContent"></div>
```